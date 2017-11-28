# Arch Linux Server Installation Step-by-Step

- To Create bootable ArchLinux in usb drive.

1. Format USB disk with MS-DOS_FAT32 and MBR in Macos/Linux Systems. 
2. Open Terminal window and run below mention command from dir. where `ArchLinux.iso` file is place.
  `sudo dd bs=4m if=archlinux_x86-64.iso of=/dev/diskX && sync`  ...(in macos bs=4M and X=1/2/3...)
3. After Finish writing the USB drive.

- To Install Arch Linux in Laptop/System.

1. Boot your laptop/system with archlinux bootable USB drive.
2. after booting enter below commands to Install Arch Linux on your system.

```
1. fdisk -l
2. cfdisk --> msdos 
  i. create partation 
    a. /dev/sda1 = 10G Type=Linux BOOT*
    b. /dev/sda2 = 2048M Type=Linux Swap
    c. /dev/sda3 = EXTENDED
        |
        |-- /dev/sda5 = ALL Type=Linux 
    d. Write Partation table and QUIT. 

3. mkfs.ext4 /dev/sda1
4. mkfs.ext4 /dev/sda5
5. mkswap /dev/sda2
6. swapon /dev/sda2
7. mount /dev/sda1 /mnt
8. mkdir /mnt/home
9. mount /dev/sda5 /mnt/home
10. pacstrap /mnt base base-devel
11. genfstab /mnt >> /mnt/etc/fstab
12. cat /mnt/etc/fstab
13. arch-chroot /mnt /bin/bash
14. vi /etc/locale.gen
  i. Insert and uncomment { en_US.UTF-8 UTF-8 }
  ii. save. {:wq }
15. locale-gen
16. vi /etc/locale.conf
  i. Insert LANG=en_US.UTF-8
  ii. save. {:wq}
17. ls /usr/share/zoneinfo
18.ln -s /usr/share/zoneinfo/{YourContinent}/{yourCity} /etc/localtime  ...(e.g. /Asia/Bangkok)
19. hwclock --systohc --utc
20. passwd  ...(change root user password.)
21. vi /etc/hostname
  i. Insert hostname as {Server01}
22. systemctl enable dhcpcd
23. pacman -S grub os-prober
24. grub-install /dev/sda
25. grub-mkconfig -o /boot/grub/grub.cfg
26. exit
27. umount /mnt/home
28. umount /mnt
29. reboot
```
                      
