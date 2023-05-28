sudo dnf install htop tmux zip unzip p7zip vim git gnome-extensions-app gnome-tweak-tool @"development tools" @"development libraries" 

# re-enable alt + right click window resize
gnome tweaks
windows
enable "resize with secondary-click"
change window action key to "alt"

# verify SSD trim is enabled
# look for fstrim.service
sudo systemctl list-timers

# dnf.conf tweaks
max_parallel_downloads=10
fastestmirror=true
