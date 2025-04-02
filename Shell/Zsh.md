
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
```bash
**If you receive "highlighters directory not found" error message,**

**you may need to add the following to your .zshenv:**

  **export ZSH_HIGHLIGHT_HIGHLIGHTERS_DIR=/opt/homebrew/share/zsh-syntax-highlighting/highlighters**
```