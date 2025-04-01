  

## .bashrc

  

Set up .bashrc for kubectl completion by adding the following:

```Plain
alias k='kubectl'

source /etc/bash_completion # not needed on macos

source <(kubectl completion bash)

complete -o default -F __start_kubectl k
```

  

## .zshrc

[https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/#enable-shell-autocompletion](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/#enable-shell-autocompletion)

Set up .zshrc on Mac for kubectl completion by adding the following:

```Plain
autoload -Uz compinit
compinit
alias k='kubectl'
source <(kubectl completion zsh)
```

  

## .vimrc

This is a basic .vimrc for YAML editing:

```Plain
" Ensure Vim uses filetype plugins
filetype plugin on

" Enable indentation
filetype indent on

" Set the default indentation to 2 spaces for all files
set tabstop=2
set softtabstop=2
set shiftwidth=2
set expandtab

" Highlight trailing whitespace in all files
autocmd BufRead,BufNewFile * match Error /\s\+$/

" Enable auto-indentation
set autoindent

" Turn on syntax highlighting
syntax on

" Set backspace so it acts more intuitively
set backspace=indent,eol,start
```

  

## Helpful links

[https://kubernetes.io/docs/reference/kubectl/quick-reference/](https://kubernetes.io/docs/reference/kubectl/quick-reference/)