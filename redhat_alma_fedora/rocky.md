# initial patching (must be done individually)
sudo dnf update -y
sudo dnf groupinstall "development tools" -y
sudo dnf install epel-release -y && sudo yum update -y
sudo dnf install 'dnf-command(copr)' -y
sudo dnf install htop tmux git vim zip unzip -y

## disable x on startup
```
sudo systemctl set-default multi-user.target
```
## enable x on startup
```
sudo systemctl set-default graphical.target
```
#

## network config
/etc/sysconfig/network-scripts/xxx
```
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=none
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
NAME=ens192
UUID=fdc66971-820c-497c-a7ba-ffc80d0f4365
DEVICE=ens192
ONBOOT=yes
IPADDR=10.9.8.99
PREFIX=24
GATEWAY=10.9.8.1
DNS1=8.8.8.8
DNS2=8.8.4.4
DNS3=1.1.1.1
IPV6_PRIVACY=no
```

