##############
## install zsh
https://www.zsh.org/
https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH

# log out and back in after installing
dnf install zsh

# run tests
zsh --version
echo $SHELL
$SHELL --version

#####################
### install oh my zsh
https://github.com/ohmyzsh/ohmyzsh

wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh
sh install.sh

## adding plugins/themes
vim ~/.zshrc

# plugins are white space delimited. No commas.
plugins=(
  git
  bundler
  dotenv
  macos
  rake
  rbenv
  ruby
)

ZSH_THEME="robbyrussell"

##########################
## install powerline fonts
https://github.com/powerline/fonts

dnf install powerline-fonts






