# UNIX SYSTEM

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

## CHMOD

cmd ==> chown
			-R 			Affecte récursivement les sous-dossiers
d: directory / l: link / r: read / w: write/ x: execute

drwxrwxrwx
-				Link or folder
 ---			Utilisateur			u (propriétaire/user)
    ---			Groupe				g (group)
       ---		Autres				o (other)

r => 4		
w => 2
x => 1

---		0	0 + 0 + 0
r--		4	4 + 0 + 0
-w-		2 	0 + 2 + 0
--x 	1	0 + 0 + 1
rw-		6	4 + 2 + 0
-wx		3	0 + 2 + 1
r-x		5	4 + 0 + 1
rwx		7	4 + 2 + 1

```
chmod 777 file 			Donne les accès à tout le monde sur un fichier/dossier
chmod g+w,o-w			Ajouter le droit d'écriture au groupe et l'enlever aux autres. 				
```

## SHELL SCRIPT

Attention au type de shell utilisé : sh (commun tout système unix), bash (commun à la plupart des sys unix), etc...

```
#!/bin/bash					# Précise quel type d'interpréteur on utilise
	  /sh

message='hello world'		# Déclare une variable liste de char

echo $message				# Affiche le message
echo -e "Ligne1\Ligne2"		# -e permet d'utiliser les retour à la ligne (\n)

message='Bonjour tout le monde'
echo 'Le message est : $message'			# Affichera => Le message est : $message



```