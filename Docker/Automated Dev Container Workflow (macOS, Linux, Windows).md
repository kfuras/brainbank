
Managing multiple Dev Containers? This setup makes it effortless to:

- Spin up Dev Containers by project type (`python`, `azure`, `kubernetes`, etc.)
- Jump into running containers by name
- Keep everything terminal-native (supports Bash, Zsh, and PowerShell)
- Automatically install config, aliases, prompt, and helper scripts

## How It Works

Just run the bootstrap script:

### On macOS/Linux:

```bash
curl -fsSL https://raw.githubusercontent.com/kfuras/dotfiles/main/bootstrap.sh | bash
```

### On Windows (PowerShell):

```powershell
irm https://raw.githubusercontent.com/kfuras/dotfiles/main/bootstrap.ps1 | iex
```

This will:

- Install [Starship](https://starship.rs/) for prompt

- Link your `.zshrc`, `.bashrc`, and Starship config

- Create devcontainer helpers:
	- `devsetup`
	- `devconnect`
	- `devshell`
- Pull `add-devcontainer` script from your [`lab`](https://github.com/kfuras/lab) repo:
    - [add-devcontainer.sh](https://github.com/kfuras/lab/blob/main/bash/add-devcontainer.sh)
    - [add-devcontainer.ps1](https://github.com/kfuras/lab/blob/main/powershell/add-devcontainer.ps1)

## Available Functions

### `devsetup <type>`

Creates a new Dev Container setup in the current folder. Supported types:

- `python`, `node`, `docker`, `bash`, `terraform`, `azure`, `kubernetes`, `docs`

```bash
devsetup python
```

### Start using VS Code

1. Open the project in VS Code:   

```bash
code .
```
When prompted, choose **“Reopen in Container”**

> Or manually via Command Palette → “Dev Containers: Reopen in Container”

This will spin up the container defined by `.devcontainer/devcontainer.json`.

### Start via CLI

If you have the `devcontainer` CLI installed (`npm install -g @devcontainers/cli`):

```bash
devcontainer up --workspace-folder .
```

Or use your helper if you add a `devbuild` function to `~/.devaliases`:

```bash
devbuild python
```

### `devconnect <project>`

Connects to a running container with name matching your project:

```bash
devconnect lab
devconnect homelab
```

### `devshell <project>`

Same as `devconnect`, but opens with `zsh` (if supported):

```bash
devshell blog-image-generator
```

### Example Folder Layout

```bash
~/code/
├── lab/                    # GitHub repo: reusable scripts and labs
├── dotfiles/              # GitHub repo: bootstrap config
├── blog-image-generator/  # Project folder with `.devcontainer/`
```

Each project will contain:

```bash
.devcontainer/
└── devcontainer.json
```

## Automatic Container Naming

Each devcontainer will be named like:

```bash
blog-image-generator-devcontainer-abc123
```
So `devconnect blog-image-generator` just works.

### Bonus: Use `fzf` to choose a container

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

## Want to use this setup?

Just run:

```bash
curl -fsSL https://raw.githubusercontent.com/kfuras/dotfiles/main/bootstrap.sh | bash
```

Or on Windows:

```powershell
irm https://raw.githubusercontent.com/kfuras/dotfiles/main/bootstrap.ps1 | iex
```

This will set everything up in one shot.

