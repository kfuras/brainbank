
This guide explains how I migrated image links in my Markdown blog posts from **inline-style** to **reference-style**, organized under a consistent folder structure (`img/`). It works great for content exported from **WordPress** or written in **Obsidian**, and targets **Hugo** (Blowfish theme in my case).

### Goal

- Move all images into a local `img/` folder inside each post directory
- Change Markdown from:
    
    `![](images/example.png)`
    
    into:
    `![][example]  ...  [example]: img/example.png`

### 1. Rename All `images/` Folders to `img/`

In your Hugo project root:

`find output/posts/* -type d -name "images" -execdir mv {} img \;`

This changes all `images/` subfolders to `img/` while keeping them in place.



### 2. Update Markdown Image Paths

We replace all `](images/...)` with `](img/...)` using `sed`:

`find output/posts -name "index.md" -exec sed -i '' 's#](images/#](img/#g' {} +`

This matches **all** alt texts, not just `![]`.



### 3. Convert Inline Images to Reference-Style (Python Script)

I used this [Python script](#) (see full version below) to scan all `index.md` files under `output/posts`, find `![alt](img/...)` patterns, and convert them into reference-style Markdown.

**Example input:**

markdown

CopyEdit

`![Diagram](img/example.png)`

**Converted to:**

markdown

CopyEdit

`![Diagram][example]  ...  [example]: img/example.png`

#### Run the script:

bash

CopyEdit

`python3 convert_inline_images.py`

---

### 🧠 What It Supports

- Inline images with or without alt text
    
- Images pasted from Obsidian (e.g. `Pasted-image-...`)
    
- Skips files without any matching links
    
- Leaves existing content untouched if already converted
    

---

### 🎯 Result

- Clean reference-style Markdown
    
- Local `img/` folders under each post
    
- Perfect for Hugo + GitHub + static publishing