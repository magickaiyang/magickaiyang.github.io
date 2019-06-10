# Trust the debug symbol signing key
debuggee$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C8CAB6595FDFF622

# Add the debug symbol repository
debuggee$ codename=$(lsb_release -c | awk  '{print $2}')
debuggee$ sudo tee /etc/apt/sources.list.d/ddebs.list << EOF
deb http://ddebs.ubuntu.com/ ${codename} main restricted universe multiverse
deb http://ddebs.ubuntu.com/ ${codename}-updates main restricted universe multiverse
deb http://ddebs.ubuntu.com/ ${codename}-proposed main restricted universe multiverse
EOF

# Retrieve the list of available debug symbol packages
debuggee$ sudo apt update

# Install the debug symbols for the current kernel version
debuggee$ sudo apt install --yes linux-image-$(uname -r)-dbgsym

mkdir ~/kernel
cd ~/kernel
sudo apt install linux-source
tar -jxvf /usr/src/linux-source-4.15.0.tar.bz2
cd linux-source-4.15.0/
sudo apt install fakeroot libncurses5-dev kernel-package

fakeroot make-kpkg

sudo vim /etc/default/grub.d/50-cloudimg-settings.cfg

rsync --recursive --relative --copy-links --verbose \
  ubuntu@192.168.122.213:/home/ubuntu/kernel/linux-source-4.15.0 :/usr/lib/debug ~/linux-source-debug
