https://www.unixarena.com/2015/12/kernel-based-virtual-machine-kvm-overview.html/

# KVM environment.  ISO, guest images, network configs, etc.
/var/lib/libvirt/images

# KVM configuration files
/etc/libvirt

# check virtualization resources
virt-top

# create pool
virsh pool-define-as pool_name dir - - - - /location

# verify creation
virsh pool-list --all

# create a new storage pool
virsh pool-build poolName

# start the storage pool
virsh pool-start poolName

# list pools
virsh pool-list --all

# get pool info
virsh pool-info poolName

# create VM
virt-install --connect qemu:///system --virt-type kvm --network bridge:br0 --name UAKVM2 --description "First RHEL7 KVM Guest" --os-variant rhel7 --ram=1024 --vcpus=1 --disk size=4 --os-type=linux --graphics vnc,password=123456 --cdrom /var/www/html/rhel-server-7.2-x86_64-dvd.iso

## find all virt-install options
 Options     | Values                | Description
====================================================================================
--connect     |qemu:///system         | Connect to the localhost KVM
--virt-type   |kvm                    | Specify the virtualization type as kvm or Xen 
--network     |bridge:br0             | Specify the bridge for network connectivity
-name         |UAKVM2                 | Virtual Machine Name
--description |First RHEL7 KVM Guest  | Provide the VM description 
--os-variant  |rhel7                  | Provide the OS-variant name
--ram         |1024                   | Set the VM memory to 1GB
--vcpus       |1                      | Set the No.of.CPU cores
-disk         |4                      | Specify the virtual disk size in GB
--os-type     |linux                  | Specify the OS type
--graphics    |vnc,password=123456    | Specify the graphics type & VNC password
--cdrom       |/path_to_iso           | Specify the RHEL 7 ISO image path


# list VMs
virsh list --all

# VM resource utilization
virt-top

# delete (halt?) the VM
virsh destroy vmName

# start a VM
virst start vmName

# KVM guest XML config files
/etc/libvirt/qemu/

# view VM's XML config
virsh dumpxml vmName

# find VM's storage path
virsh dumpxml UAKVM2 |grep -i "source file"

# install a VM on another host
virt-install --connect qemu+ssh://root@192.168.203.134/system --virt-type kvm --network bridge:br0 --name UAKVM2 --description "First RHEL7 KVM Guest" --os-variant rhel7 --ram=1024 --vcpus=1 --disk size=4 --os-type=linux --graphics vnc,password=123456 --cdrom /var/www/html/rhel-server-7.2-x86_64-dvd.iso

# suspend a VM
virsh suspend vmName
virsh list --all

# clone VM
virt-clone --connect qemu:///system --original UAKVM2 --name UACLONE --file /var/lib/libvirt/images/UACLONE.qcow2

# resume a VM
virsh resume vmName

# sysprep a cloned/copied VM
virt-sysprep -d vmName
virt-sysprep --list-operations
virt-sysprep -d UACLONE  --hostname UACLONE --root-password password:123456

# launch virt console (on GUI/X?)
virt-viewer 28

# view VM device mappings
virsh domblklist UAKVM2 --details

# attach a LUN to a VM
virsh attach-disk UAKVM2 --source /dev/sdb --target vdb --persistent

# create QCOW image
qemu-img create -f qcow2 UAKVM2.disk2.qcow2 1G

# create QCOW image - raw format, thin
qemu-img create -f raw UAKVM2.disk3.img 256M

# create IMG image - raw format, thick
dd if=/dev/zero of=UAKVM2.disk4.img bs=1M count=1000

# show virtual disks in storage pool
du -sh UAKVM2.disk*

# attach a disk to a VM
virsh attach-disk UAKVM2 --source /var/lib/libvirt/images/UAKVM2.disk2.qcow2 --target vdc --persistent
virsh domblklist UAKVM2 --details

# increase virtual disk size
virsh qemu-monitor-command UAKVM2 --hmp "block_resize drive-virtio-disk2 2G"
xfs_growfs /orastage/

# view VM memory settings
virsh dumpxml  UAKVM2|grep -i memo

# view domain config of a VM
virsh dominfo UAKVM2

# change memory settings of a VM
virsh setmem vmName 512M

# change memory settings of a VM (persistent)
virsh setmem UAKVM2 2048M --config
virsh edit vmName

# set VM maximum memory
# stop the VM
virsh setmaxmem vmName 4G

# set VM CPU's
virsh setvcpus vmName 2

# set VM CPU's (persistent)
virsh setvcpus vmName 2 --config

# change virtual CPU's of a live system
virsh setvcpus --live --guest vmName 1
virsh setvcpus --config UAKVM2 1
virsh setvcpus UAKVM2 3

# start a VM
virsh start vmName

# change VM image storage path
# shut down running VMs
# verify/change SELINUX.  Changing path might set off alerts.

# check existing storage pool
virsh pool-dumpxml default |grep -i path

# verify there are VM's at the default path
virsh vol-list default |grep "/var/lib/libvirt/images"

# stop the default storage pool
virsh pool-destroy default

# modify the pool path
virsh pool-edit default

# start the pool
virsh pool-start default

# verify the pool path
virsh pool-dumpxml default |grep -i path

# move VM's and images to new path
mv /var/lib/libvirt/images/UAKVM2.qcow2 /kvmpool/

# modify the VM config
source file='/kvmpool/UAKVM2.qcow2'

# start the VM
# check for SELINUX errors
virsh start vmName

# live migrations
https://www.unixarena.com/2015/12/perform-live-migration-on-linux-kvm.html/


