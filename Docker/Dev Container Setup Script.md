
This script creates a `.devcontainer` folder in your project with a working `devcontainer.json` tailored to the type of project you're working on.

## Supported Types

- `python` – Python projects with `requirements.txt`

- `node` – Node.js projects with `npm install`

- `docker` – Docker-in-Docker for container tools

- `bash` – Simple script-based setups

- `terraform` – Infrastructure-as-code with Terraform

- `docs` – Markdown/documentation projects

- `azure` – Azure CLI, PowerShell, Az module, Bicep CLI

- `kubernetes` – Kubernetes tools including `kubectl`, `helm`, YAML

## Usage

From inside your repo:

```bash

./add-devcontainer.sh --type=python

```

You can omit the `--type` to default to `python`.

## Adding Support for More Languages

To add more languages or stack types:

1. Open the script and locate the `case "$PROJECT_TYPE" in` block

2. Add a new case like this:

```bash

go)

cat >> "$DEV_FOLDER/devcontainer.json" <<EOF

"image": "mcr.microsoft.com/devcontainers/go:latest",

"postCreateCommand": "apt update && apt install -y neovim",

EOF

;;

```

3. Run the script with your new type:

```bash

./add-devcontainer.sh --type=go

```

This will generate a `devcontainer.json` using the base image and optional tools for Go.

## Shared Configuration

All generated containers include:

- Basic VS Code extensions:

- Neovim integration

- Prettier

- Spell checker

- YAML/Kubernetes extensions

- Font folder mount from host for custom fonts (optional)

## Output

Each run will generate or overwrite:

- `.devcontainer/devcontainer.json`

- `requirements.txt` (for Python, if missing)

You can add this to version control:

```bash

git add .devcontainer requirements.txt

git commit -m "chore: add devcontainer for <type>"

```

## File

Save the script as `add-devcontainer.sh` and make it executable:

```bash

chmod +x add-devcontainer.sh

```
