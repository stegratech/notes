https://ostechnix.com/download-rpm-package-dependencies-centos/
https://unix.stackexchange.com/questions/220503/how-to-install-dependencies-of-an-rpm-package-without-installing-the-package-its
https://unix.stackexchange.com/questions/232946/how-to-copy-all-files-from-a-directory-to-a-remote-directory-using-scp

https://access.redhat.com/solutions/45956
(Pasted below)

###

yumdownloader --resolve @"development tools"


yum deplist bind | awk '/provider:/ {print $2}' | sort -u |   xargs yum -y install

yum deplist *.rpm | awk '/provider:/ {print $2}' | sort -u |   xargs yum update --downloadonly
yum deplist *.rpm | awk '/provider:/ {print $2}' | sort -u |   xargs yum reinstall --downloadonly --downloaddir /tmp/rpms/dependencies2/

yum --disablerepo=* localinstall ./*.rpm

# repeat yumdownloader as neededed for dependencies

###

Resolution
Different scenarios of updating an offline system are discussed in How can we regularly update the system without internet connection ?

If none of the methods mentioned in the above article work, you can update an offline system by using a online system to download the RPMs from and copy them over to the offline system.

1) On the online/connected system: Verify that the required packages are installed for downloading the RPMs:

Raw
Install yum-utils for Red Hat Enterprise Linux 7 , yum-plugin-downloadonly for Red Hat Enterprise Linux 6 or yum-downloadonly and yum-utils for Red Hat Enterprise Linux 5 on the machine which is connected to the Internet or any repository:
Note: The repository needs to be enabled on the online system for that system to be able to download the packages, you can verify this with the command # yum repolist

2) Copy the RPM db from the offline system to the online system (This could also be copied to a USB drive):

Raw
# tar cjf rpm_db.tar.bz2 /var/lib/rpm
# scp rpm_db.tar.bz2 root@online:/tmp/
3) Extract the database on the online system into an empty directory

Raw
# mkdir /tmp/rpm_db/
# tar xf /tmp/rpm_db.tar.bz2 -C /tmp/rpm_db/
4) On the online system download all the RPM packages

Raw
# yum update --downloadonly --downloaddir /tmp/rpm_db --installroot=/tmp/rpm_db/
5) Copy the downloaded rpm updates from the online system to the offline system (This could also be copied to a USB drive)

Raw
# tar cjf rpm-updates.tar.bz2 /tmp/rpm_db/*.rpm
# scp rpm-updates.tar.bz2 root@offline:/tmp/
# ssh root@offline
# mkdir /tmp/rpms
# tar xf /tmp/rpm-updates.tar.bz2 -C /tmp/rpms
6) Update the offline system

Raw
## see above to ignore repos
# yum localinstall /tmp/rpms/*.rpm


