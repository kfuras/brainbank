
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

```powershell
devsetup python
```

### `devconnect <project>`

Connects to a running container with name matching your project:

```powershell
devconnect lab
devconnect homelab
```

### `devshell <project>`

Same as `devconnect`, but opens with `zsh` (if supported):