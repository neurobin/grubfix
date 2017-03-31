A bash script to fix the grub menu.

# Usage:

Simply run the script:

```bash
sudo bash ./grubfix
```

It will give you a list of partition to select from:

```bash
**********************************************************
 Please choose the device where your system is installed. 
 A star (*) sign after the device id means it's bootable  
 It is not necessary for a system partition to be bootable
 Be carefule. We need the device id where the filesystem  
 resides, not where it is booted from.                    
**********************************************************

1) /dev/sda5        251662336  775949445  524287110   250G 83 Linux
2) /dev/sda9        775952384  985667583  209715200   100G 83 Linux
3) /dev/sdb1  *          2048  118947360  118945313  56.7G 83 Linux
4) /dev/sdb3       3268208640 3907022847  638814208 304.6G 83 Linux
5) /dev/sdb8       3058259968 3268208639  209948672 100.1G 83 Linux
6) exit
Choose a device (#?): 
```

Choose the device from the list where your system is installed.

It will ask for confirmation:

```bash
*** you have chosen: /dev/sdb1

*** Giving more info for confirmation

*** 'fdisk -l /dev/sdb1' says: 
Disk /dev/sdb1: 56.7 GiB, 60900000256 bytes, 118945313 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes

*** 'blkid /dev/sdb1' says: 
/dev/sdb1: UUID="7ede5dce-6e56-4642-b9f4-86f16200d8e9" TYPE="ext4" PARTUUID="8ea4fe84-01"

=== Please confirm (Y/n)?: 
```
Confirm with 'y' if it's really the right device id.

```bash
*** /dev/sdb1 confirmed...

*** mounted /dev/sdb1 in /mnt

*** mounted /dev in /mnt/dev

*** mounted /dev/pts in /mnt/dev/pts

*** mounted /proc in /mnt/proc

*** mounted /sys in /mnt/sys

*** running grub-install /dev/sdb ...
Installing for i386-pc platform.
Installation finished. No error reported.

*** running update-grub ...
Generating grub configuration file ...
Found background image: /usr/share/images/desktop-base/desktop-grub.png
Found linux image: /boot/vmlinuz-4.9.0-2-amd64
Found initrd image: /boot/initrd.img-4.9.0-2-amd64
Found linux image: /boot/vmlinuz-3.16.0-4-amd64
Found initrd image: /boot/initrd.img-3.16.0-4-amd64
Found memtest86+ image: /boot/memtest86+.bin
Found memtest86+ multiboot image: /boot/memtest86+_multiboot.bin
Found Windows 10 on /dev/sda1
Found Xubuntu 16.04 LTS (16.04) on /dev/sda9
done

*** unmounted /mnt/sys

*** unmounted /mnt/proc

*** unmounted /mnt/dev/pts

*** unmounted /mnt/dev

*** unmounted /mnt
```

**If it's more complex than that, then this script also allows you to open a chroot terminal on your target system**, run it with `-co` option:

```bash
sudo bash ./grubfix -co
```

It will not do any additional task other than opening a terminal window with chroot. You can then use that terminal to configure your target system and install or modify pacakges to correct problems.

