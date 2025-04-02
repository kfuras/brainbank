Absolutely! Here's the **fully formatted Markdown text**, ready to copy and paste directly into **Obsidian** (or anywhere else). It includes fenced code blocks (` ``` `), blank lines for proper rendering, and no raw HTML.

---

````markdown
# 🧠 Dev Container Shell Aliases for Multi-Repo Workflows

If you're managing multiple projects using Dev Containers (like `lab`, `homelab`, `python`), you can create reusable terminal aliases to quickly connect to the right running container.

This guide helps you:

- Create smart CLI functions to connect to running dev containers  
- Name your containers per project  
- Use the setup across multiple repositories  

---

## ✅ Step 1: Add Shell Functions

Create a file called `~/.devaliases`:

```bash
# ~/.devaliases

# Connect to a container by name
devconnect() {
  container=$(docker ps --filter "name=$1" --format "{{.Names}}" | head -n 1)

  if [ -z "$container" ]; then
    echo "❌ No container found matching: $1"
    return 1
  fi

  echo "🔗 Connecting to $container ..."
  docker exec -it "$container" bash
}

# (Optional) Build a devcontainer from code folder
devbuild() {
  devcontainer up --workspace-folder ~/code/$1
}

# (Optional) Connect using zsh instead of bash
devshell() {
  container=$(docker ps --filter "name=$1" --format "{{.Names}}" | head -n 1)

  if [ -z "$container" ]; then
    echo "❌ No container found matching: $1"
    return 1
  fi

  docker exec -it "$container" zsh
}
````

Then source it in your `.zshrc` or `.bashrc`:

```bash
[ -f ~/.devaliases ] && source ~/.devaliases
```

---

## ✅ Step 2: Name Your Dev Container per Project

Edit your `.devcontainer/devcontainer.json`:

```json
{
  "name": "lab",
  "image": "mcr.microsoft.com/devcontainers/python:3.11"
}
```

This ensures the running container includes a project-specific name like `lab-devcontainer-xyz123`.

---

## 📦 Example Repo Structure

```
~/code/
├── homelab/
│   └── .devcontainer/ (name = "homelab")
├── lab/
│   └── .devcontainer/ (name = "lab")
├── python/
│   └── .devcontainer/ (name = "python")
```

Now use these from anywhere:

```bash
devconnect lab
devconnect homelab
devconnect python
```

---

## 🧠 Bonus: Interactive Container Picker (Optional)

Install `fzf`, then replace `devconnect` with:

```bash
devconnect() {
  container=$(docker ps --format "{{.Names}}" | fzf)

  if [ -z "$container" ]; then
    echo "❌ No container selected"
    return 1
  fi

  docker exec -it "$container" bash
}
```

---

## 📁 Suggested Folder for Obsidian

Place this note in your vault under:

```
brainbank/
└── devcontainers/
    └── aliases-and-connect.md
```

✅ You’re now set up to move between containers across all your projects using one command.

```

---

✅ Paste the above directly into Obsidian — it will render perfectly with code blocks and headings.

Let me know if you want me to turn this into a templated snippet for all future container projects too!
```