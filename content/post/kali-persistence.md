+++
title = "Kali Persistence"
date = 2017-12-31T02:06:13-05:00
draft = true
comments = true
categories = ["Security OS", "Tools"] 
description = "" 
tags = ["encryption", "kali", "persistence"]
image = "/img/kali-persistence/kali-persistence.jpg"

+++

## Kali Persistence

The name of the indian goddess Kali is particularly well choosen for a pentesting distribution. She is a figure of duality that we describe as a loving mother and a blood thirsty warrior. She inspired a group of assassins named the Thuggee between the 14th and 19th centuryans bcame more rencontly a figurehead of resistance and female empowerment by westerners. 

---

The Kali live mode is much more powerfull in my opinion with persistence. This allow the user to download programs beforehanda nd easilly bring files and collect data on site. In this article I will show you how to install Kali Linux with persistence and LUKS-encryption. 
</br>

### Portable Kali Linux with persistence
 
1. Get root with `sudo -i`. Make a bootable usb key of the latest version of Kali Linux. A quick way to achive this `mkfs.vfat -I /dev/sdb && dd if=/home/lotana/Downloads/kali-linux-2017.3-amd64.iso of=/dev/sdb bs=10M`

2. Let's use parted to resize the primary partition to make space for the persistence storage `end=$(($(blockdev --getsize64 /dev/sdb)/ 1000000)) && start=$(du -bm /home/lotana/Downloads/kali-linux-2017.3-amd64.iso | cut -f1) && parted /dev/sdb mkpart primary $start $end`

3. Choose a password for encryption `cryptsetup --verbose --verify-passphrase luksFormat /dev/sdb3 && cryptsetup luksOpen /dev/sdb3 usb`

4. Label the new partition as "persistence" `mkfs.ext4 -L persistence /dev/mapper/usb && e2label /dev/mapper/usb persistence`

4. The followinf commands will make the media persistent`mkdir -p /mnt/usb && mount /dev/mapper/usb /mnt/usb && echo "/ union" > /mnt/usb/persistence.conf && umount /dev/mapper/usb`. You can then close the encrypted channel to the persistent drive with `cryptsetup luksClose /dev/mapper/usb`.  

6. Boot on the usb stick and choose the persistent mode with encryption. You can still see the persistent drive mounted on the desktop? Open a terminal inside the persistent drive and do `echo "/ union" > ./persistence.conf`. After that, or if the persistent drive is not visible, do `gsettings set org.gnome.nautilus.desktop volumes-visible false` to avoid the Kali Live drive to be mounted on the desktop on startup.  
</b>