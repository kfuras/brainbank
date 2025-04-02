When working with Git, renaming folders or files manually (via Finder or `mv`) doesn’t automatically tell Git what you did — instead, it sees this as:

- Deleted files from the old path

- New untracked files in the new path


This can cause confusing errors during `git push` or `git pull --rebase`.

### Symptoms You Might See

- `git status` shows a bunch of deleted files

- `git push` fails with a message like:

`Updates were rejected because the remote contains work that you do not have locally.`

- `git pull` fails with:    

`error: cannot pull with rebase: You have unstaged changes.`


## Steps to Safely Rename Folders and Files in Git

### 1. **Rename the folder or files manually**

`mv blog_image_generator blog-image-generator`

### 2. **Stage both the deletions and the new files**

This will tell Git what’s changed:

```bash
git add -u  # Stages deleted (removed) files 
git add .   # Stages all new files and folder structure
```

### 3. **Commit the rename**

`git commit -m "refactor: rename blog_image_generator to blog-image-generator"`

### 4. **Rebase if needed**

If your push fails because the remote has changes:

`git pull origin main --rebase git push`

## Bonus: Watch for `.gitignore` mismatches

If you rename a folder (e.g., `generated_images/` → `generated-images/`) but forget to update `.gitignore`, Git might accidentally track the contents.

### Fix:

1. Update `.gitignore` to match the new name:

`generated-images/`

2. Remove the now-tracked folder (but keep files locally):

`git rm -r --cached generated-images/ git commit -m "chore: fix .gitignore to match renamed folder" git push`


## Summary

|Task|Command|
|---|---|
|Stage deleted files|`git add -u`|
|Stage new files|`git add .`|
|Untrack a folder|`git rm -r --cached <folder>`|
|Fix ignored folder|Update `.gitignore`|
|Clean push flow|`git pull origin main --rebase && git push`|