# Add users, change passwords, set permissions
https://pve.proxmox.com/wiki/User_Management
http://candramiladre.blogspot.com/2016/10/solved-change-password-failed-user.html

useradd steve
passwd steve
cat /etc/group | grep -i watch
groupadd watchman
usermod -aG watchman steve
vim /etc/passwd
vim /etc/group
pveum groupadd -FPKIAdmin - comment "FPKI Admins"
pveum groupadd FPKIAdmin -comment "FPKI Admins"
pveum aclmod / -group FPKIAdmin -role Administrator
pveum usermod steve@proxmox1 -group FPKIAdmin
pveum usermod steve -group FPKIAdmin
pveum usermod steve@pve -group FPKIAdmin
pveum
pveum user modify
pveum usermod steve@pam -group FPKIAdmin

# repositories
https://pve.proxmox.com/wiki/Package_Repositories

# set up free licensing
https://lunar.computer/posts/no-subscription-proxmox-60/

cd /etc/apt/sources.list.d
mv pve-enterprise.list pve-enterprise.list.disabled
vi pve-no-subscription.list
deb http://download.proxmox.com/debian/pve bullseye pve-no-subscription
apt-get update && apt-get dist-upgrade -y
pveupgrade


# change repositories
sudo mv /etc/apt/sources.list.d/pve-enterprise.list /etc/apt/sources.list.d/pve-enterprise.list.disabled
sudo echo "deb http://download.proxmox.com/debian/pve bullseye pve-no-subscription" > /etc/apt/sources.list.d/pve-no-subscription.list
sudo apt update
sudo pveupgrade

# storage directories
https://pve.proxmox.com/wiki/Storage:_Directory

VM images : images/<VMID>/
ISO images : template/iso/
Container templates : template/cache/
Backup files : dump/
Snippets : snippets/

# adding storage
https://pve.proxmox.com/wiki/Storage

# add storage
https://s55ma.radioamater.si/2019/07/23/adding-a-new-hard-drive-to-proxmox-and-then-mounting-it-to-lxc-linux-container/
https://www.virtualizor.com/docs/admin/add-new-storage/
https://www.hostfav.com/blog/index.php/2017/02/01/add-a-new-physical-hard-drive-to-proxmox-ve-4x-5x/

# extend storage
https://forum.proxmox.com/threads/extend-lvm-shared-storage.50811/

# ZFS
https://pve.proxmox.com/wiki/ZFS:_Tips_and_Tricks

# adding NFS
https://pve.proxmox.com/wiki/Storage:_NFS

# guest additions
https://pve.proxmox.com/wiki/Qemu-guest-agent
https://access.redhat.com/solutions/732773

Have to completely power down the guest for agent to work.

apt-get install qemu-guest-agent
yum install qemu-guest-agent

