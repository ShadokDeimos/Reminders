
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

## Manually install package .deb

> install all .deb file
``sudo dpkg -i *.deb``

> the following command processes in a single pass the .deb of the directory where the command is launched as well as those of the subdirectories
``sudo dpkg -i `find . -type f -name '*.deb'` ``

> -R option recursively install all packages in working directory and subdirectories
``sudo dpkg -i -R *.deb``

> dpkg don't manage dependencies, following command complete app installation dependencies
 ``sudo apt-get -f install``

> following command fix dependencies problems
``sudo apt --fix-broken install``