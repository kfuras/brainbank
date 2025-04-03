
## Recommended `.zshrc` (Personal File)

You can add this to your `~/.zshrc` **above** the `# >>> dotfiles <<<` block:

```bash
# Load Zsh plugins manually
# Ensure these are installed via Homebrew (or manually in ~/.zsh)
if [ -f /opt/homebrew/share/zsh-autosuggestions/zsh-autosuggestions.zsh ]; then
  source /opt/homebrew/share/zsh-autosuggestions/zsh-autosuggestions.zsh
fi

if [ -f /opt/homebrew/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh ]; then
  source /opt/homebrew/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
fi

if [ -f /opt/homebrew/share/zsh-completions/zsh-completions.zsh ]; then
  source /opt/homebrew/share/zsh-completions/zsh-completions.zsh
fi

# Ensure correct completion init
autoload -Uz compinit
compinit

# Use Starship for prompt
eval "$(starship init zsh)"

```

## 💻 Install required tools via Homebrew:

```bash
brew install zsh-autosuggestions
brew install zsh-syntax-highlighting 
brew install zsh-completions
```

Then reload:

```bash
source ~/.zshrc
```

## Example `.zshrc`

```bash
# dotfiles/.zshrc

# History settings
HISTFILE=~/.zsh_history
HISTSIZE=10000
SAVEHIST=10000

# Editor
export EDITOR=nvim

# Enable command auto suggestions (if zsh-autosuggestions is installed)
if [ -f /opt/homebrew/share/zsh-autosuggestions/zsh-autosuggestions.zsh ]; then
  source /opt/homebrew/share/zsh-autosuggestions/zsh-autosuggestions.zsh
fi

# Enable completions (if zsh-completions is installed)
if [ -f /opt/homebrew/share/zsh-completions/zsh-completions.zsh ]; then
  fpath+=("/opt/homebrew/share/zsh-completions")
  autoload -Uz compinit && compinit
fi

# Starship prompt
eval "$(starship init zsh)"

# Custom aliases (optional)
alias k=kubectl
alias tf="terraform"
alias gs="git status"

# Source aliases if present
[ -f ~/.devaliases ] && source ~/.devaliases

```