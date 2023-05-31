add EPEL repository
```
yum install epel-release -y
```
#
equivalent of build essential
```
sudo yum groupinstall 'Development Tools' -y
sudo yum install automake gcc gcc-c++ kernel-devel cmake python-devel python3-devel NetworkManager-tui -y
```
#
enable extras (RHEL)
```
yum-config-manager --enable rhui-REGION-rhel-server-extras rhui-REGION-rhel-server-optional
yum install [https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm](https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm)
subscription-manager repos --enable "rhel-*-optional-rpms" --enable "rhel-*-extras-rpms"
```
#
disable x on startup
```
systemctl set-default multi-user.target
```
#
enable x on startup
```
systemctl set-default graphical.target
```
#
query all installed packages
```
sudo rpm -qa
sudo rpm -q vim-enhanced
yum list installed | grep -i vim
```

##

# give non-root users ability to run a command
vi /etc/sudoers
user    ALL=(root) NOPASSWD: /usr/bin/yum update root

# set hostname
hostnamectl set-hostname xxx

# show installed version
https://www.tecmint.com/check-centos-version/
cat /etc/centos-release
cat /etc/redhat-release
cat /etc/fedora-release

##
# create new user
useradd example_user && passwd example_user

# add them to wheel/sudo
usermod -aG wheel example_user

##
# temporarily disable selinx
setenforce permissive

# check selinux status
sestatus

# watch selinux log for blocked access
tail -f /var/log/audit/audit.log

# disable selinux
vim /etc/sysconfig/selinux

##
# NETWORKING
BOOTPROTO=static
DEFROUTE=yes
PEERDNS=yes
PEERROUTES=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_PEERDNS=yes
IPV6_PEERROUTES=yes
IPV6_FAILURE_FATAL=no
NAME=ens18
UUID=c81bdc2d-e22a-4360-afe4-cc8e8f571a1c
DEVICE=ens18
ONBOOT=yes
IPADDR=192.168.1.12
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
DNS1=8.8.8.8
DNS2=208.67.222.222

# set hostname
hostnamectl set-hostname xxx







## Configure Default Gateway (optional)
#
# vi /etc/sysconfig/network

NETWORKING=yes
HOSTNAME=centos6
GATEWAY=192.168.1.1

## Configure DNS Server (optional)
#
# vi /etc/resolv.conf

nameserver 8.8.8.8      # Replace with your nameserver ip
nameserver 192.168.1.1  # Replace with your nameserver ip


## Restart Network Interface
#

/etc/init.d/network restart

##
# FIREWALL

# list zone configuration
firewall-cmd --list-all
firewall-cmd --zone=home --list-all
firewall-cmd --list-all-zones | less

# list all zones
firewall-cmd --get-zones

# change the zone for an interface (temporary)
sudo firewall-cmd --zone=home --change-interface=eth0

# change the zone for an interface (permanent)
vim /etc/sysconfig/network-scripts/ifcfg-eth0
# add to file
ZONE=home

# restart networking and firewall
sudo systemctl restart network.service
sudo systemctl restart firewalld.service

# change default zone
sudo firewall-cmd --set-default-zone=home

# list all available services
firewall-cmd --get-services

# list services in use
firewall-cmd --list-services

# where services are stored
# create a custom service (restart firewall after creation)
/usr/lib/firewalld/services/ssh.xml

# add a service (temp)
sudo firewall-cmd --zone=public --add-service=http

# add a service (permanent)
sudo firewall-cmd --zone=public --add-service=http --permanent
sudo firewall-cmd --zone=public --add-service=dhcp --permanent
sudo firewall-cmd --add-service=ssh9922 --permanent
sudo firewall-cmd --zone=public --add-service=snmp --permanent

# add port instead of service - have to reload firewall
sudo firewall-cmd --zone=public --add-port=5000/tcp --permanent
sudo firewall-cmd --zone=public --add-port=4990-4999/udp --permanent

sudo firewall-cmd --add-port=5601/tcp --permanent
sudo firewall-cmd --add-port=5601/udp --permanent
sudo firewall-cmd --add-port=5601/tcp --permanent

##
# YUM FASTEST MIRROR
https://wiki.centos.org/PackageManagement/Yum/FastestMirror

yum install yum-plugin-fastestmirror

After fastestmirror is installed, make sure that it is enabled. Edit the file /etc/yum/pluginconf.d/fastestmirror.conf and ensure that it contains the following lines:

[main]
verbose = 0
socket_timeout = 3
enabled = 1
hostfilepath = /var/cache/yum/timedhosts.txt
maxhostfileage = 1

##
# SYSTEMD
https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files

# location
/etc/systemd/system

# unit types
.service	A system service.
.target	A group of systemd units.
.automount	A file system automount point.
.device	A device file recognized by the kernel.
.mount	A file system mount point.
.path	A file or directory in a file system.
.scope	An externally created process.
.slice	A group of hierarchically organized units that manage system processes.
.snapshot	A saved state of the systemd manager.
.socket	An inter-process communication socket.
.swap	A swap device or a swap file.
.timer	A systemd timer.

##
# SERVICES
https://www.cyberciti.biz/faq/check-running-services-in-rhel-redhat-fedora-centoslinux/

# show all services/sockets
systemctl list-units 

# check if it is enabled
systemctl is-enabled frobozz

# list enabled services
systemctl list-unit-files | grep -i enabled

systemctl --type=service -all

systemctl -all | grep -i cockpit



