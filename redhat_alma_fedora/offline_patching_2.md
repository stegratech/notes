https://ostechnix.com/download-rpm-package-dependencies-centos/
https://unix.stackexchange.com/questions/220503/how-to-install-dependencies-of-an-rpm-package-without-installing-the-package-its
https://unix.stackexchange.com/questions/232946/how-to-copy-all-files-from-a-directory-to-a-remote-directory-using-scp

https://access.redhat.com/solutions/45956

###

1. Get the RPM db from the offline system

# tar cjf rpm_db.tar.bz2 /var/lib/rpm

2. Copy to Aegis and copy and extract to /tmp on the online system

# mkdir /tmp/rpm_db/
# tar xf /tmp/rpm_db.tar.bz2 -C /tmp/rpm_db/

3. Download the RPM's using the offline db

# yum update --downloadonly --downloaddir /tmp/rpm_db --installroot=/tmp/rpm_db/

4. Pack up the RPM's and download/move to Aegis

# tar cjf rpm-updates.tar.bz2 /tmp/rpm_db/*.rpm

5. Copy and unpack the RPM's on the offline system

# mkdir /tmp/rpms
# tar xf /tmp/rpm-updates.tar.bz2 -C /tmp/rpms

6. Update the offline system

# yum localinstall /tmp/rpms/*.rpm
or
# yum --disablerepo=* localinstall ./*.rpm

####
Missing dependencies?

# Download specific packages/dependencies
yumdownloader --resolve @"development tools"

# Download dependencies based on apps or RPM's

# Specific app
yum deplist bind | awk '/provider:/ {print $2}' | sort -u |   xargs yum -y install

# Based on RPM's
yum deplist *.rpm | awk '/provider:/ {print $2}' | sort -u |   xargs yum update --downloadonly --downloaddir /tmp/rpm_db
yum deplist *.rpm | awk '/provider:/ {print $2}' | sort -u |   xargs yum reinstall --downloadonly --downloaddir /tmp/rpm_db

