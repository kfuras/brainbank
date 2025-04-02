
## Install required tools via Homebrew:

```bash
brew install zsh-autosuggestions
brew install zsh-syntax-highlighting
brew install zsh-completions
```

To activate the syntax highlighting, add the following at the end of your .zshrc:

```bash
source /opt/homebrew/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

If you receive `highlighters directory not found` error message, you may need to add the following to your .zshenv:

```bash
export ZSH_HIGHLIGHT_HIGHLIGHTERS_DIR=/opt/homebrew/share/zsh-syntax-highlighting/highlighters
```

To activate these completions, add the following to your .zshrc:

```bash
if type brew &>/dev/null; then

    FPATH=$(brew --prefix)/share/zsh-completions:$FPATH

    autoload -Uz compinit
    compinit

fi
```

You may also need to force rebuild `zcompdump`:

```bash
  rm -f ~/.zcompdump; compinit
```

Additionally, if you receive `zsh compinit: insecure directories` warnings when attempting
to load these completions, you may need to run these commands:

```bash
  chmod go-w '/opt/homebrew/share'
  chmod -R go-w '/opt/homebrew/share/zsh'
```

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

```b
`brew install zsh-autosuggestions brew install zsh-syntax-highlighting brew install zsh-completions`

```
Then reload:

`source ~/.zshrc`