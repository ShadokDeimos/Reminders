# LINUX-TIPS

## Make windows disk part writable from ubuntu

sudo mount -o remount,rw '/media/SGTL MSCN'

=> Install disk-manager by download package
	=> install dependencies.
Select hard drive part you want mount (select ntfs-3g) for reads permissions

> On windows partition 
- Launch PowerShell with admin's rights
- type ``powercfg -h off``