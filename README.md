
  Mount UBS Drive for Proxmox Backup


Mount UBS Drive for Proxmox Backup
✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨
YouTube Mount UBS Drive for Proxmox Backup 🔗 https://youtu.be/lZjMxdBPH7M
✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨
SUPPORT MY WORK - Everything Helps Thanks YouTube 🔗 https://YouTube.GetMeTheGeek.com
Buy Me a Coffee ☕ https://www.buymeacoffee.com/getmethegeek
Hire US 🔗 https://getmethegeek.com
Digital Ocean referral 🔗 https://tiny.cc/plxdigitalocean
✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨✨

Find the USB Drive

Plug USB drive into Proxmox host machine.
```wrap
lsblk
lsusb
fdisk -l
mkdir /mnt/usb-drive 
/etc/fstab
ls -l /dev/disk/by-uuid/*
```
#Format USB drive EXT4
```wrap
mkfs.ext4 /dev/sde1
blkid -o list
```
Make directory to mount usb drive
```wrap
mkdir /mnt/usb-drive
```
Setup Permanent Mount

In order to mount your USB drive permanently after reboot add a line into your /etc/fstab config file. If drives are added or removed from the Proxmox the device may change. For this reason the partion UUID will need to be used instead of the block device name.
```wrap
ls -l /dev/disk/by-uuid/*
lrwxrwxrwx 1 root root 13 Jun 30 10:50 /dev/disk/by-uuid/169C06729C064CA5 -> ../../zd128p1
lrwxrwxrwx 1 root root 10 Sep  7 08:23 /dev/disk/by-uuid/1C9696109695EA92 -> ../../sde1
lrwxrwxrwx 1 root root 10 Jun 30 10:50 /dev/disk/by-uuid/4331501758443482231 -> ../../sdd2
lrwxrwxrwx 1 root root 12 Jun 30 10:50 /dev/disk/by-uuid/46FF7800EE8FFB6D -> ../../zd96p1
```
Above will give you the uuid. Open the fstab for editing
```wrap
nano /etc/fstab
```
Add this line to your fstab using the correct UUID.
```wrap
/dev/disk/by-uuid/1C9696109695EA92    /mnt/usb-drive         ext4   defaults   0
```
Mount drive
```wrap
mount -a
