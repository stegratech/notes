## download ISO
https://www.debian.org/CD/http-ftp/

## add user to sudoers
**run as root, log off and log on as user**
```
usermod -aG sudo steve
```

## sources.list generator
https://debgen.xyz/


## update the apt repositories
```
# deb cdrom:[Debian GNU/Linux 11.6.0 _Bullseye_ - Unofficial amd64 DVD Binary-1 with firmware 20221217-10:46]/ bullseye contrib main non-free
# deb cdrom:[Debian GNU/Linux 11.6.0 _Bullseye_ - Unofficial amd64 DVD Binary-1 with firmware 20221217-10:46]/ bullseye contrib main non-free

deb http://security.debian.org/debian-security bullseye-security main contrib non-free
deb-src http://security.debian.org/debian-security bullseye-security main contrib non-free

# bullseye-updates, to get updates before a point release is made;
# see https://www.debian.org/doc/manuals/debian-reference/ch02.en.html#_updates_and_backports
# A network mirror was not selected during install.  The following entries
# are provided as examples, but you should amend them as appropriate
# for your mirror of choice.
#
# deb http://deb.debian.org/debian/ bullseye-updates main contrib non-free
# deb-src http://deb.debian.org/debian/ bullseye-updates main contrib non-free

deb https://deb.debian.org/debian/ bullseye-updates main contrib non-free
deb-src https://deb.debian.org/debian/ bullseye-updates main contrib non-free

deb https://deb.debian.org/debian/ bullseye main contrib non-free
deb-src https://deb.debian.org/debian/ bullseye main contrib non-free

deb https://deb.debian.org/debian-security bullseye-security main contrib non-free
deb-src https://deb.debian.org/debian-security bullseye-security main contrib non-free
```

## update system
```
sudo apt-get update
sudo apt-get dist-upgrade -y
sudo apt-get install htop ssh build-essential zip unzip p7zip vim tmux gdebi git wget curl -y
```
## disable x on startup
```
systemctl set-default multi-user.target
```
## enable x on startup
```
systemctl set-default graphical.target
```
