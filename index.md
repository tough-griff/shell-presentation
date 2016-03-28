title: Getting To Know Your Shell
author:
  name: Griffin Yourick
  url: github.com/tough-griff
output: index.html
style: style.css

--

# Getting To Know Your Shell
## Tips and tricks for a better development process

--

### Aliases and Functions

If you find yourself using it often, add it!
```sh
alias ls='ls -h --color=auto --group-directories-first'
alias ll='ls -l'
alias la='ll -a'
```

Functions are necessary when anything comes after the arguments, e.g.,
```sh
# Grep within `ps`, filtering out the `grep` process.
function psg {
  ps aux | grep $@ | grep -v grep
}
```

--

### .gitconfig

[github/hub](https://github.com/github/hub) is a helpful tool for integrating
the `git` CLI with github.com.

`brew install hub` and add `eval "$(hub alias -s)"` to your startup script.

___

[so-fancy/diff-so-fancy](https://github.com/so-fancy/diff-so-fancy) is an
improved `git diff`.

`brew install diff-so-fancy` and add the following to your .gitconfig:
```
[pager]
  diff = diff-so-fancy | less
  show = diff-so-fancy | less
```

See the
[README](https://github.com/so-fancy/diff-so-fancy/blob/master/readme.md) for
additional configuration recommendations.

--

### .gitconfig cont'd

Other recommended configs:
```
# Global gitignore.
[core]
  excludesfile = ~/.gitignore

# Nice log format.
[format]
  pretty = "%C(red)%h%C(reset) -%C(yellow)%d%C(reset) %s %C(green)(%cr)%C(reset) %C(bold blue)<%an>%C(reset)"

# Always use HTTPS git.
[url "https://github.com/"]
  insteadOf = git://github.com/
  insteadOf = git@github.com:
  insteadOf = ssh://git@github.com:

[url "https://git.heroku.com/"]
  insteadOf = git://heroku.com/
  insteadOf = git@heroku.com:
  insteadOf = ssh://git@heroku.com:
```

--

### git + aliases?

Why not? Here are some for you to try:
```sh
alias g='git'
alias ga='git add -A'
alias gc='git commit --message'
alias gd='git diff'
alias gdc='git diff --cached'
alias gl='git log --graph'
alias gp='git push'
alias gpl='git pull'
alias gs='git status --short'
alias gsh='git show'
```

You type these *a lot*. Save yourself hundreds of keystrokes in the first few
days!

--

### Get comfortable with brew

`brew` is your best friend.

`brew update && brew upgrade --all` often.

If it's command line, `brew search` for it first.

For apps, try `brew cask`

--

### The OS X Script

The legendary
[~/.osx](https://github.com/mathiasbynens/dotfiles/blob/master/.osx) script
comes from
[Mathias Bynens's dotfiles](https://github.com/mathiasbynens/dotfiles) repo
which has over 13,500 stars. It has great defaults for optimizing your machine.

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

**[Completions](https://github.com/tough-griff/dotfiles/blob/master/zsh/completion.zsh)**
```sh
brew install zsh-completions
```
___

**[History and Higlighting](https://github.com/tough-griff/dotfiles/blob/master/zsh/highlighting_and_history.zsh)**
```sh
brew install zsh-history-substring-search
brew install zsh-syntax-highlighting
```
___

[oh-my-zsh](http://ohmyz.sh/) is a great resource if you don't want to spend
hours tweaking and installing your own extensions and plugins.

--

### GNUtilities

`ls -G` in BSD vs. `ls --color=auto` in GNU

For consistency:
```sh
brew install coreutils findutils moreutils gawk gnu-sed
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

[clvv/fasd](https://github.com/clvv/fasd) is a tool for quickly accessing files
and directories.

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
