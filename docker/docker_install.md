# install docker desktop on Ubuntu/Debian-based distro
https://docs.docker.com/desktop/install/debian/
https://docs.docker.com/desktop/install/ubuntu/


https://docs.docker.com/engine/install/debian/#set-up-the-repository

# install pre-requisites
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release -y

# add docker GPG key (debian)
sudo mkdir -m 0755 -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# add docker GPG key (ubuntu)
sudo mkdir -m 0755 -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# add the repo (debian)
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# add the repo (ubuntu)
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# install the docker desktop app
# download docker desktop
https://docs.docker.com/desktop/install/debian/
https://docs.docker.com/desktop/install/ubuntu/

sudo apt-get update
sudo gdebi ./xxx-docker-desktop.deb

# test install
docker version
docker info

