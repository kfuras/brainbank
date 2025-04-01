**Category:** `Automation`

**Tags:** `Developer Workflow`, `Python`, `Pillow`

### Introduction

Creating a featured image for every blog post used to be the most tedious part of publishing for me. I wanted each post to look visually consistent, but opening Canva, copying/pasting the title, and exporting it over and over again got old fast.

So… I automated it.

Now I generate my 1200×628px featured images using a Python script in seconds — with a background, styled title, category label, and even my domain in the corner.

In this post, I’ll show you exactly how I do it using Python and the [Pillow](https://pypi.org/project/Pillow/) library.

### Why Automate Featured Images?

- All my blog cards look aligned and branded
- It takes me 5 seconds to create 5+ images
- No more messing with manual layouts

This setup gives me more time to focus on content — not design.

### Tools Used

- Python 3 (preinstalled on macOS/Linux)
- [Pillow](https://pypi.org/project/pillow/) (Python Imaging Library)
- A font (`Roboto-Bold.ttf`)
- A custom background image (made in [Canva](https://www.canva.com/))
- A CSV file with blog post titles

### The Python Code

Here’s the core script that powers everything. You can drop it into a file like `generate_images.py`:

```Python
from PIL import Image, ImageDraw, ImageFont
import csv, os

WIDTH, HEIGHT = 1200, 628
BACKGROUND_IMAGE = "background.jpg"
FONT_PATH = "Roboto-Bold.ttf"
FONT_SIZE = 48
SMALL_FONT_SIZE = 24
OUTPUT_DIR = "generated_images"
TEXT_COLOR = "white"
CATEGORY_LABEL = "Automation"

os.makedirs(OUTPUT_DIR, exist_ok=True)

font = ImageFont.truetype(FONT_PATH, FONT_SIZE)
small_font = ImageFont.truetype(FONT_PATH, SMALL_FONT_SIZE)

with open("titles.csv", newline='') as csvfile:
    reader = csv.DictReader(csvfile)
    for row in reader:
        title = row.get("title", "").strip()
        if not title:
            continue

        bg = Image.open(BACKGROUND_IMAGE).resize((WIDTH, HEIGHT))
        img = bg.convert("RGB")
        draw = ImageDraw.Draw(img)

        draw.text((40, 30), CATEGORY_LABEL, font=small_font, fill="\#94a3b8")

        # Basic word wrapping
        words = title.split()
        lines, line = [], ""
        for word in words:
            test = f"{line} {word}".strip()
            if draw.textlength(test, font=font) < WIDTH - 100:
                line = test
            else:
                lines.append(line)
                line = word
        lines.append(line)

        y_start = (HEIGHT - len(lines) * FONT_SIZE) // 2
        for i, line in enumerate(lines):
            text_width = draw.textlength(line, font=font)
            x = (WIDTH - text_width) // 2
            y = y_start + i * FONT_SIZE
            draw.text((x, y), line, font=font, fill=TEXT_COLOR)

        # Save image
        safe_name = title.lower().replace(" ", "_").replace("/", "-")
        img.save(os.path.join(OUTPUT_DIR, f"{safe_name}.png"))

```

### High-Level Overview of What the Script Does

The logic is pretty straightforward:

1. **Loads your background image** and resizes it to 1200×628px
2. **Reads blog post titles** from a CSV file (`titles.csv`)
3. **Wraps long titles** into multiple lines if needed
4. **Draws a category label** in the top-left corner
5. **Centers the title text** on the image
6. **Saves the output** as `.png` files in a `generated_images` folder

It uses a Python library to draw text on the image and create blog-ready graphics.

### Your Input CSV File

Create a `titles.csv` file with this structure:

```Shell
title
Install Roboto Fonts on macOS with Intune
Disable Password Prompt for sudo
Deploy Bicep Templates via Azure CLI
```

Then run the script with:

```Shell
python3 generate_images.py
```

You should see the following output if the code ran with success:

```Shell
🖼️ Generating image for: Install Roboto Fonts on macOS with Intune
✅ Saved: generated_images/install_roboto_fonts_on_macos_with_intune.png
```

That’s it — one image per blog title, saved and ready to upload.

### Full Source Code on GitHub

Want the full working setup — including the script, sample CSV file, background template, and font reference?

You can grab everything here:

👉 [github.com/kfuras/featured-image-generator](https://github.com/kfuras/featured-image-generator)

### Final Thoughts

This tiny automation has saved me a surprising amount of time. If you’re a developer who writes regularly, I highly recommend automating repetitive tasks like design and formatting. It’s a small boost that compounds over time — and keeps your workflow fun.