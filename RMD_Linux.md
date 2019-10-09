

### Version

cat /etc/debian_version       version de debian
uname -a                      version du kernel

## Static Ipv4 Network

auto ens33
allow-hotplug ens33
iface ens33 inet static
  address xxx.xxx.xxx.xxx
  netmask xxx.xxx.xxx.xxx
  broadcast xxx.xxx.xxx.xxx
  gateway xxx.xxx.xxx.xxx

## External Access

$ nano /etc/resolv.conf

 -> Add this two lines
$ nameserver 8.8.8.8
$ nameserver 8.8.4.4
 -> Save file
