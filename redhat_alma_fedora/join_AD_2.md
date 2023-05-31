#####
# join linux server to AD
# restrict access to server using groups
# restrict access to sudo/wheel using groups
# realm is a wrapper for adcli
#####

## 1 - install dependencies
sudo dnf install samba-common-tools realmd oddjob oddjob-mkhomedir sssd adcli krb5-workstation authconfig

## 2 - update polices and reboot
sudo update-crypto-policies --set DEFAULT:AD-SUPPORT

## 3 - perform pre-tests before joining AD

# verify DNS points to AD
dig -t SRV _ldap._tcp.home.zzz

# verify/discover the AD domain
adcli info home.zzz
realm discover home.zzz

## 4 - join AD
realm join --automatic-id-mapping=no ad.example.com -U other_username

## 5 - configure kerberos settings for AD domain
# sudo vim /etc/krb5.conf

# To opt out of the system crypto-policies configuration of krb5, remove the
# symlink at /etc/krb5.conf.d/crypto-policies which will not be recreated.
includedir /etc/krb5.conf.d/

[logging]
default = FILE:/var/log/krb5libs.log
kdc = FILE:/var/log/krb5kdc.log
admin_server = FILE:/var/log/kadmind.log

[libdefaults]
# dns_lookup_realm = false
dns_lookup_realm = true
ticket_lifetime = 24h
renew_lifetime = 7d
forwardable = true
rdns = false
pkinit_anchors = FILE:/etc/pki/tls/certs/ca-bundle.crt
spake_preauth_groups = edwards25519
dns_canonicalize_hostname = fallback
qualify_shortname = ""
default_realm = HOME.ZZZ
default_ccache_name = KEYRING:persistent:%{uid}
# udp_preference_limit = 0
udp_preference_limit  = 1
default_realm = HOME.ZZZ
dns_lookup_kdc = true

[realms]
HOME.ZZZ =
{
	kdc = dc1.home.zzz
	admin_server = dc1.home.zzz
}
	
[domain_realm]
.home.zzz = HOME.zzz
home.zzz = HOME.ZZZ


## 6 - configure ??

# old command - authselect replaces authconfig
sudo authconfig --enablesssd --enablesssdauth --enablelocauthorize --enablemkhomedir --update

sudo authselect select sssd with-mkhomedir

## 7 - configure sssd
sudo vim /etc/sssd/sssd.conf


[sssd]
domains = home.zzz
config_file_version = 2
services = nss, pam

[domain/home.zzz]
default_shell = /bin/bash
krb5_store_password_if_offline = True
cache_credentials = True
krb5_realm = HOME.ZZZ
realmd_tags = manages-system joined-with-adcli
id_provider = ad
fallback_homedir = /home/%u@%d
ad_domain = home.zzz
use_fully_qualified_names = True
ldap_id_mapping = False
access_provider = ad
override_homedir = /home/%d/%u
debug_level = 0

# Uncomment and configure below , if service discovery is not working 
# ad_server = server.win.example.com

[nss]
override_shell=/bin/bash

[pam]


##  8 - set SSSD permissons
sudo chown root:root /etc/sssd/sssd.conf
sudo chmod 600 /etc/sssd/sssd.conf

## 9 - enable sssd service and start
sudo systemctl enable sssd --now

## 10 - test connectivity
