If you're managing multiple projects in Dev Containers, jumping between them quickly is key.

This guide shows you how to:

- Create reusable aliases to connect to containers by name

- Name your Dev Containers properly

- Keep your workflow smooth and terminal-native

### Why This Rocks

- No more remembering long container names

- Works across any project

- Zero friction to enter your container shell and run `vim`, `nvim`, or whatever you want

- Compatible with Docker, Docker Compose, and Dev Containers

## 1. Add Shell Functions for Your Workflow

Create a file called `~/.devaliases`:

```bash

# ~/.devaliases

# Connect to a running container by name
devconnect() {
  container=$(docker ps --filter "name=$1" --format "{{.Names}}" | head -n 1)

  if [ -z "$container" ]; then
    echo "❌ No container found matching: $1"
    return 1
  fi

  echo "🔗 Connecting to $container ..."
  docker exec -it "$container" bash
}

# (Optional) Build/launch a dev container project by folder
devbuild() {
  devcontainer up --workspace-folder ~/code/$1
}

# (Optional) Connect using Zsh
devshell() {
  container=$(docker ps --filter "name=$1" --format "{{.Names}}" | head -n 1)

  if [ -z "$container" ]; then
    echo "❌ No container found matching: $1"
    return 1
  fi

  docker exec -it "$container" zsh
}

```

### Add to `.zshrc` or `.bashrc`:

```bash
[ -f ~/.devaliases ] && source ~/.devaliases
```

Reload your shell:

```bash
source ~/.zshrc # or source ~/.bashrc
```

## 2. Name Your Dev Container per Project

To make your container discoverable by `devconnect`, **name it uniquely** inside each repo.

### For `.devcontainer/devcontainer.json`:

```bash
{
  "name": "lab",
  "image": "mcr.microsoft.com/devcontainers/python:3.11",
  ...
}
```

This will name the container something like:

```
lab-devcontainer-123abc
```

Which means `devconnect lab` will find it.

## 3. Repo Structure Example

Let’s say you have:

```bash
~/code/
├── homelab/
│   └── .devcontainer/
│       └── devcontainer.json (name = "homelab")
├── lab/
│   └── .devcontainer/
│       └── devcontainer.json (name = "lab")
├── python/
│   └── .devcontainer/
│       └── devcontainer.json (name = "python")
```

Now, in any terminal window:

```bash
devconnect lab
# Connects to the lab container

devconnect homelab
# Switches to the homelab container

devconnect python
# Same again, super clean

```

## Optional: Use `fzf` for selection

If you have many containers, you can make `devconnect` interactive:

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