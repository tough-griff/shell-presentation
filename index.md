title: Getting To Know Your Shell
author:
  name: Griffin Yourick
  url: github.com/tough-griff
output: index.html

--

# Getting To Know Your Shell
## Tips and tricks for a better development process

--

### ZSH

`zsh` is everything `bash` and more.

```sh
brew install zsh
sudo echo "$(brew prefix)/bin/zsh" >> /etc/shells
chsh -s $(brew prefix)/bin/zsh
```

--

### Some ZSH Extensions

[**Completions**](https://github.com/tough-griff/dotfiles/blob/master/zsh/completion.zsh)
```sh
brew install zsh-completions
```

GIF

**[History and Higlighting](https://github.com/tough-griff/dotfiles/blob/master/zsh/highlighting_and_history.zsh)**
```sh
brew install zsh-history-substring-search
brew install zsh-syntax-highlighting
```

GIF

--

### GNUtilities
**BSD**
```sh
ls -G           # BSD
ls --color=auto # GNU
```

For consistency:
```sh
brew install coreutils findutils moreutils
brew install gawk gnu-sed
```

[gnu_utils.zsh](https://github.com/tough-griff/dotfiles/blob/master/zsh/gnu_utils.zsh)
```sh
where ls
ls () {
	'/usr/local/bin/gls' "$@"
}
```

--

### Getting around FASD
`brew install fasd`

```sh
# .zshrc
fasd_cache="$HOME/.fasd-init-zsh"
if [ "$(command -v fasd)" -nt "$fasd_cache" -o ! -s "$fasd_cache" ]; then
  eval "$(fasd --init posix-alias zsh-hook zsh-ccomp zsh-ccomp-install zsh-wcomp zsh-wcomp-install)" >| "$fasd_cache"
fi
source "$fasd_cache"
unset fasd_cache
```
