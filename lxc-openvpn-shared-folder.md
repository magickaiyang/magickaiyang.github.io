# Install LXC
sudo apt install lxc

# Prepare for unprivileged container
/etc/lxc/lxc-usernet
your-username veth lxcbr0 10

Create the ~/.config/lxc directory if it doesn't exist.
Copy /etc/lxc/default.conf to ~/.config/lxc/default.conf
Append the following two lines to it:
lxc.idmap = u 0 100000 65536
lxc.idmap = g 0 100000 65536

# Create a privileged container named "c1"
lxc-create -t download -n c1

# add to config
lxc.mount.entry = /dev/net/tun dev/net/tun none bind,create=file
lxc.mount.entry = /path/to/folder/on/host /path/to/mount/point none bind 0 0

chmod -R go+w /folder/to/share

# install common packages
sudo apt install iptables software-properties-common curl
