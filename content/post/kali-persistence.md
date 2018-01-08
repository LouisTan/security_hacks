+++
title = "Kali Linux with Persistence"
date = 2017-12-31T02:07:13-05:00
draft = false
comments = true
categories = ["Security OS", "Tools"] 
description = "" 
tags = ["encryption", "kali", "persistence"]
image = "/img/kali-persistence/kali-persistence.jpg"

+++

## Kali Linux with Persistence

The Kali live mode is much more useful with persistence. It permits you to download programs beforehand, bring files and collect data on site. You will also have access to the forensic mode wich allows you to boot in a computer mode without modifying the hard drive in any way. In this article I will show you how to make a  Kali Linux bootable usb with persistence and LUKS-encryption. I would suggest you to invest in the latest protocol of usb for this since it is going to make data transfers a lot faster. 
</br>

### Kali Linux with persistent storage and LUKS encryption
 
1. Find the device that corresponds to the usb key on wich you want to install Kali Linux with `lsblk`. It may be /dev/sdb but don't take my word for granted. 

2. Get root with `sudo -i`. Make a bootable usb key of the latest version of Kali Linux. A quick way to achive this `mkfs.vfat -I /dev/sdb && dd if=/home/lotana/Downloads/kali-linux-2017.3-amd64.iso of=/dev/sdb bs=10M`.

3. Let's use parted to resize the primary partition to make space for the persistence storage `end=$(($(blockdev --getsize64 /dev/sdb)/ 1000000)) && start=$(du -bm /home/lotana/Downloads/kali-linux-2017.3-amd64.iso | cut -f1) && parted /dev/sdb mkpart primary $start $end`.There are other ways to do this, using gparted by instance. It is more visual and simpler to operate but I wanted use only the terminal for this tutorial.

4. Choose a password for encryption `cryptsetup --verbose --verify-passphrase luksFormat /dev/sdb3 && cryptsetup luksOpen /dev/sdb3 usb`.

5. Label the new partition as "persistence" `mkfs.ext4 -L persistence /dev/mapper/usb && e2label /dev/mapper/usb persistence`.

6. The following commands will make the media persistent `mkdir -p /mnt/usb && mount /dev/mapper/usb /mnt/usb && echo "/ union" > /mnt/usb/persistence.conf && umount /dev/mapper/usb`. You can then close the encrypted channel to the persistent drive with `cryptsetup luksClose /dev/mapper/usb`. Boot on the usb stick and choose the persistent mode with encryption. If you see the persistent drive mounted on the desktop, that means we did not merge the drives. If this is the case, just open a terminal inside the persistent drive and do `echo "/ union" > ./persistence.conf`. 

7. After that, or if the persistent drive wasn't visible on the desktop, do `gsettings set org.gnome.nautilus.desktop volumes-visible false` to avoid the Kali live drive to be mounted on startup.Don't forget to `apt-get update`. Don't forget to change the root user with `passwd`. You might want to save you work by cloning your drive with Clonezilla.  
</br>