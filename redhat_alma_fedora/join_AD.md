https://access.redhat.com/solutions/2653771

### join a server to AD
# install dependencies
sudo yum install samba-common-tools realmd oddjob oddjob-mkhomedir sssd adcli krb5-workstation authconfig

# update polices and reboot
update-crypto-policies --set DEFAULT:AD-SUPPORT

# confirm records can be resolved
dig -t SRV _ldap._tcp.adexample.net

# discover the AD domain
adcli info ad.example.com

### join AD

# join AD the normal way
adcli join ad.example.com
adcli join ad.example.com -U other_username

# join AD over LDAPS/636
LDAPTLS_CACERT=<cert path> adcli join --use-ldaps <domain_name> -U <username> --verbose

# another way?
realm join --automatic-id-mapping=no ad.example.com

## configure krb5.com to use AD domain
# /etc/krb5.conf

[libdefaults]
default_realm = AD.EXAMPLE.COM
dns_lookup_realm = true
dns_lookup_kdc = true
ticket_lifetime = 24h
renew_lifetime = 7d
forwardable = true
udp_preference_limit  = 1

[realms]
AD.EXAMPLE.COM = {
kdc = server.ad.example.com
admin_server = server.ad.example.com
}

[domain_realm]
.ad.example.com = AD.EXAMPLE.COM
ad.example.com = AD.EXAMPLE.COM


### configure name server switch
# using authconfig
authconfig --enablesssd --enablesssdauth --enablelocauthorize --enablemkhomedir --update

# using authselect
authselect select sssd with-mkhomedir

#################################################
## configure sssd
# /etc/sssd/sssd.conf

[sssd]
services = nss, pam
config_file_version = 2
domains = AD.EXAMPLE.COM

[domain/AD.EXAMPLE.COM]
id_provider = ad
override_homedir = /home/%d/%u
debug_level = 0
# Uncomment and configure below , if service discovery is not working 
# ad_server = server.win.example.com

[nss]
override_shell=/bin/bash

[pam]

# set SSSD permissons
sudo chown root:root /etc/sssd/sssd.conf
sudo chmod 600 /etc/sssd/sssd.conf

# start and enable sssd
sudo systemctl sssd enable --now

#################################################
#### test connectivity
id ad_user
ssh ad_user@localhost

realm discover ad.example.com

getent passwd administrator@ad.example.com

#################################################
#### restrict access

### add AD groups to sudoers

## find the group names/memberships for a user
id username

## add the group to sudo/wheel
sudo vim /etc/sudoers

or

sudo visudo

# add the group
%groupname ALL=(ALL) ALL



