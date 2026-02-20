
2026-02-15 23:06

Status:

Tags:[[VM]] 

# VM Setup
This will be a note of how to install a VM and to set it up with the needed packages.

### First steps
su - to enter sudo
apt install sudo
usermod -aG deadlywhisp3r

sudo apt install xrdp -> install remote desktop for better gui access
sudo systemctl enable xrdp -> to enable it on start of the VM
sudo systemctl start xrdp

* sudo apt-get install curl
* sudo apt install git -y
	* git is a requirement for installing homebrew
* /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"


# References
