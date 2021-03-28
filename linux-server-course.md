# Linux Server Course - System Configuration and Operation
My notes following [freecodecamp Linux Server Course](https://www.youtube.com/watch?v=WMy3OzvBWc0&feature=emb_logo)

## Booting 

* BIOS and UEFI, both is way how to interact between HW and operating system 
* BIOS - basic input output system
  * first sector on disk, MBR (master boot record), tell us where the partitions are and where to boot 
  * using BIOS and MBR only 4 partitions are possible 
  * limitation on how large can the partision be 
* UEFI - unified extensible firmware interface 
  * replacement for BIOS, instead of boot sector there is a whole boot partition with boot code 
  * number of partisions not limited
  * supports secure boot (BIOS doesnt)


* GRUB - GNU GRand Unified Bootloader
  * transition from BIOS/UEFI to operating system
  * GRUB "Legacy"
  * if you find *menu.lst* or *grub.conf* in `boot/grub` you are using GRUB
  * boot menu usually displays on boot
* GRUB2 
  * if you find *grub.cfg* you are using GRUB2
  * customizable with *grub.cfg*
  * can boot from USB, ISO... 
  * hidden boot menu (press shift)


Linux has a lot of boot methods, for example
* PXE (Preboot Execution Environment), linux booting over a network 
  * HW is set to ignore harddrive, query a network DHCP server and it responds not only with IP address but also with a boot file and tftp location 
  * iPXE, similar, instead of tftp it can use http 
* booting from ISO that is not on CD or USB, just on a disk

Testing DNS - all those doing the same thing
* dig @server (optional) host 
* nslookup host server (optional) 
* host host server (optional)
  * host tell us also email address 



Standart linux network configuration files (all having something to do with DNS) are
* /etc/hosts
  * first resolt DNS lookup, it looks here before quering DNS server 
  * we can add stuff here, for example `127.0.0.1 google.com` will forward all people trying to reach google to localhost (show error)
* /etc/resolv.conf
* /etc/nsswitch.conf 
Other configuration files differs between distributions.



