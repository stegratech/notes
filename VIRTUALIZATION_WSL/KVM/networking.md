ifcfg-br1
#
DEVICE="br1"
ONBOOT="yes"
TYPE="Bridge"
BOOTPROTO="none"
IPADDR="192.168.1.88"
GATEWAY="192.168.1.1"
STP="on"
DELAY="0.0"

###
ifcfg-eno1
#
DEVICE=eno1
ONBOOT=yes
BRIDGE="br1"

