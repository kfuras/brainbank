
Managing multiple Dev Containers? This guide helps you:

- Quickly enter any container via name
- Set up new projects with one command
- Keep everything terminal-native
- Avoid remembering long container IDs

## What You Get

- Simple aliases for `devsetup`, `devconnect`, and `devshell`
- Consistent DevContainer naming per project
- No need to remember container IDs
- Works across Unix/macOS + Windows (WSL/PowerShell)

---

## 1. Enable Dev Container Functions

### On Unix/macOS

Your aliases live in `~/.devaliases` and are auto-loaded via `.zshrc` or `.bashrc`.

These functions are created by the `dotfiles/bootstrap.sh` script:

```bash
# ~/.devaliases

devsetup() {
  "$HOME/bin/add-devcontainer" --type="$1"
}

devconnect() {
  container=$(docker ps --filter "name=$1" --format "{{.Names}}" | head -n 1)
  if [ -z "$container" ]; then
    echo "❌ No container found matching: $1"
    return 1
  fi
  docker exec -it "$container" bash
}

devshell() {
  container=$(docker ps --filter "name=$1" --format "{{.Names}}" | head -n 1)
  if [ -z "$container" ]; then
    echo "❌ No container found matching: $1"
    return 1
  fi
  docker exec -it "$container" zsh
}
```

Make sure this is in your `.zshrc` or `.bashrc`:

[ -f ~/.devaliases ] && source ~/.devaliases
