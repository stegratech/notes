## remove snap
https://haydenjames.io/remove-snap-ubuntu-22-04-lts/

## list installed snaps
snap list

## stop snap services
sudo systemctl disable snapd.service

sudo systemctl disable snapd.socket

sudo systemctl disable snapd.seeded.service

## remove each snap
sudo snap remove xx

## delete leftover snap stuff
sudo rm -rf /var/cache/snapd/

## purge snapd 
sudo apt autoremove --purge snapd

## remove anything left in home directory
rm -rf ~/snap
