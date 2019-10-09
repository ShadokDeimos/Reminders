
# LINUX REPOSITORY

## Modify Repository Link

nano /etc/apt/sources.list

## Debian Jessie

### Debian Jessie, dépôt principal
deb http://deb.debian.org/debian/ jessie main
### Debian Jessie, mises à jour de sécurité
deb http://security.debian.org/ jessie/updates main

apt update



## FUCK SHITTY APT UPDATE

nano -w /etc/resolv.conf
nameserver 8.8.8.8
nameserver 8.8.4.4
