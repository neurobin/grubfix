A bash script to fix the grub menu.

# Usage:

Simply run the script:

```bash
sudo ./grubfix
```

It will guide you step by step:

```bash
**********************************************************
 Please choose the device where your system is installed. 
 A star (*) sign after the device id means it's bootable  
 It is not necessary for a system partition to be bootable
 Be careful. We need the device id where the filesystem  
 resides, not where it is booted from.                    
**********************************************************

1) /dev/sdb3  148510720 206970879  58460160 27.9G Linux filesystem
2) /dev/sdb4  206970880 264634367  57663488 27.5G Linux filesystem
3) /dev/sdb6  383746048 500103167 116357120 55.5G Linux filesystem
4) exit
Choose a device (#?): 2

*** you have chosen: /dev/sdb4

*** Giving more info for confirmation

*** 'fdisk -l /dev/sdb4' says: 
Disk /dev/sdb4: 27.5 GiB, 29523705856 bytes, 57663488 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes

*** 'blkid /dev/sdb4' says: 
/dev/sdb4: UUID="c0664c62-699d-4a8e-ae2f-81ee87975527" TYPE="ext4" PARTLABEL="Basic data partition" PARTUUID="6c56a7a0-b9b0-01d4-d043-2830d85cea00"

=== Please confirm (Y/n)?: y

*** /dev/sdb4 confirmed...
***********************************************************
 Please choose the uefi boot device.
 Be careful, we need the device id where it is booted from,
 not where the root filesystem resides.
***********************************************************

1) /dev/sda1        2048    1333247    1331200   650M EFI System
2) /dev/sdb1       2048   1333247   1331200  650M EFI System
3) No uefi
4) exit
Choose a efi device (#?): 1

*** you have chosen: /dev/sda1

*** Giving more info for confirmation
Partition 1 does not start on physical sector boundary.
Partition 2 does not start on physical sector boundary.
Partition 3 does not start on physical sector boundary.

*** 'fdisk -l /dev/sda1' says: 
Disk /dev/sda1: 650 MiB, 681574400 bytes, 1331200 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x69737369

Device      Boot      Start        End    Sectors   Size Id Type
/dev/sda1p1      1869771365 2038460886  168689522  80.4G 69 unknown
/dev/sda1p2      1701519481 3571400945 1869881465 891.6G 73 unknown
/dev/sda1p3            2573       2573          0     0B 74 unknown
/dev/sda1p4      2885681152 2885733566      52415  25.6M  0 Empty

Partition table entries are not in disk order.

*** 'blkid /dev/sda1' says: 
/dev/sda1: LABEL="ESP" UUID="9382-8550" TYPE="vfat" PARTLABEL="Basic data partition" PARTUUID="93828d50-bca4-01d4-a842-c149525eea00"

=== Please confirm (Y/n)?: y

*** /dev/sda1 confirmed...

*** mounted /dev/sdb4 in /mnt

*** mounted /dev in /mnt/dev

*** mounted /dev/pts in /mnt/dev/pts

*** mounted /proc in /mnt/proc

*** mounted /sys in /mnt/sys

*** chroot: running mount /dev/sda1 /boot/efi ...

*** chroot: running grub-install ...
Installing for x86_64-efi platform.
Installation finished. No error reported.

*** chroot: running update-grub ...
Generating grub configuration file ...
Found theme: /usr/share/grub/themes/manjaro/theme.txt
Found linux image: /boot/vmlinuz-4.19-x86_64
Found initrd image: /boot/intel-ucode.img /boot/initramfs-4.19-x86_64.img
Found initrd fallback image: /boot/initramfs-4.19-x86_64-fallback.img
Found Ubuntu 18.04.2 LTS (18.04) on /dev/sdb3
Found memtest86+ image: /boot/memtest86+/memtest.bin
done

*** chroot: running umount /boot/efi

*** unmounted /mnt/sys

*** unmounted /mnt/proc

*** unmounted /mnt/dev/pts

*** unmounted /mnt/dev

*** unmounted /mnt

```

**If it's more complex than that, then this script also allows you to open a chroot terminal on your target system**, run it with `-co` option:

```bash
sudo ./grubfix -co
```

In chroot only mode, it will not do any additional task other than opening a terminal window with chroot. You can then use that terminal to configure your target system and install or modify pacakges to correct problems.

