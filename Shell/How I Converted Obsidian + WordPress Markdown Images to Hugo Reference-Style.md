
This guide explains how I migrated image links in my Markdown blog posts from **inline-style** to **reference-style**, organized under a consistent folder structure (`img/`). It works great for content exported from **WordPress** or written in **Obsidian**, and targets **Hugo** (Blowfish theme in my case).

### Goal

- Move all images into a local `img/` folder inside each post directory

Change Markdown from:

```markdown
 ![](images/example.png)
```

Into:

```markdown
![][example]  
...  
[example]: img/example.png
```

### 1. Rename All `images/` Folders to `img/`

In your Wordpress export root:

```bash
find output/posts/* -type d -name "images" -execdir mv {} img \;
```

This changes all `images/` subfolders to `img/` while keeping them in place.

### 2. Update Markdown Image Paths

We replace all `](images/...)` with `](img/...)` using `sed`:
```bash
find output/posts -name "index.md" -exec sed -i '' 's#](images/#](img/#g' {} +
```

This matches **all** alt texts, not just `![]`.

### 3. Convert Inline Images to Reference-Style (Python Script)

I used this **Python script** (see full version below) to scan all `index.md` files under `output/posts`, find `![alt](img/...)` patterns, and convert them into reference-style Markdown.

**Example input:**

```markdown
![Diagram](img/example.png)
```

**Converted to:**

```markdown
![Diagram][example]  
...  
[example]: img/example.png
```

### Create the script:

```bash
mkdir -p convert-inline-images
cd convert-inline-images
nvim convert_inline_images.py
```

```python
import os
import re

# 🔧 Set your absolute path to Hugo content posts
# This version expands `~` to your home directory and avoids path confusion
POSTS_DIR = os.path.expanduser("~/code/wordpress-export-to-markdown/output/posts")

# ✅ Match both ![Alt](img/foo.png) and ![](img/foo.png)
INLINE_IMAGE_PATTERN = re.compile(r'!\[([^\]]*)]\((img/[^)]+)\)')

def convert_images_in_file(filepath):
    with open(filepath, 'r', encoding='utf-8') as f:
        content = f.read()

    matches = INLINE_IMAGE_PATTERN.findall(content)

    # 🔍 Debug info
    print(f"🕵️ Scanning: {filepath}")
    if matches:
        print(f"   🎯 Found {len(matches)} inline image(s)")
    else:
        print(f"   ❌ No inline image matches found")
        return False

    used_refs = set()
    replacements = {}
    ref_lines = []

    for alt_text, path in matches:
        ref_label = os.path.splitext(os.path.basename(path))[0]
        ref_label = ref_label.replace(" ", "-").lower()

        # Avoid duplicate reference labels
        original_label = ref_label
        i = 2
        while ref_label in used_refs:
            ref_label = f"{original_label}-{i}"
            i += 1
        used_refs.add(ref_label)

        replacements[f'![{alt_text}]({path})'] = f'![{alt_text}][{ref_label}]'
        ref_lines.append(f"[{ref_label}]: {path}")

    # Replace inline images
    for old, new in replacements.items():
        content = content.replace(old, new)

    # Add references to end if not already present
    if ref_lines:
        content += "\n\n" + "\n".join(ref_lines) + "\n"

    with open(filepath, 'w', encoding='utf-8') as f:
        f.write(content)

    return True

def main():
    converted_files = 0
    for root, dirs, files in os.walk(POSTS_DIR):
        for file in files:
            if file == "index.md":
                full_path = os.path.join(root, file)
                if convert_images_in_file(full_path):
                    print(f"✅ Converted: {full_path}")
                    converted_files += 1

    print(f"\n🎉 Done. {converted_files} file(s) updated.")

if __name__ == "__main__":
    main()
```
### Run the script:

In your `convert-inline-images/` root:
```bash
python3 convert_inline_images.py
```

### What It Supports

- Inline images with or without alt text
- Images pasted from Obsidian (e.g. `Pasted-image-...`)
- Skips files without any matching links
- Leaves existing content untouched if already converted

### Result

- Clean reference-style Markdown
- Local `img/` folders under each post
- Perfect for Hugo + GitHub + static publishing