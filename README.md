# kobo-mini-dual-boot
Android
-------
http://www.mobileread.com/forums/showthread.php?t=244000
https://www.dropbox.com/s/8pfqgriu85miz7i/2014-08-07_Android_Kobo_Touch_public.7z

Linux
-----
https://pan.baidu.com/s/1jG44Mxw#path=%252FDebianAndroid-DualBoot
debian-android.8GiB.raw.img.7z 


16G sd card with partition table
p1 contains linux (taken from the debian-android image for the aura)
p2 contains android system (taken from the kobo touch image Marek Gibek provided)
p3 contains android data (taken from the kobo touch image Marek Gibek provided)
p6 contains vfat partition (taken from the kobo touch image Marek Gibek provided)


/dev/mmcblk1p1         19456 12600000 12580545     6G 83 Linux
/dev/mmcblk1p2      12600001 14500000  1900000 927.8M 83 Linux
/dev/mmcblk1p3      14500001 18500000  4000000   1.9G 83 Linux
/dev/mmcblk1p4      18500001 31275000 12775000   6.1G  5 Extended
/dev/mmcblk1p5      18503680 19500000   996321 486.5M 82 Linux swap / Solaris
/dev/mmcblk1p6      19503104 31275000 11771897   5.6G  b W95 FAT32




partition-table-linux.txt (provided in this repository)
sfdisk -f /dev/mmcblk1 < /usr/src/partition-table-linux.txt 


To switch between android and linux, I execute a script which writes an image to the first 19456 blocks
(linux-boot.img and android-boot.img can be found in this repository)

(under android open terminal and su root)
/Android Data/data/boot-linux
dd if=linux-boot.img of=/dev/block/mmcblk0
---mounting vfat---
mount /dev/block/mmcblk0p6 /mnt/sdcard

linux (execute as root password root)
under /root/androidboot
dd if=android-boot.img of=/dev/mmcblk0
