## Topic 102: Linux Installation and Package Management

## 102.1 Design hard disk layout
- decoding file types
- first letter is type 
  - `-` regular file
  - `d` directory 
  - `l` symbolic link
  - >> A symbolic link, or symlink, is a special type of file whose function is to link to another file, which may be of any type: a regular file, a directory, another symlink, etc. The first letter l of the metadata string lrwxrwxrwx also identifies the file as a symlink. The letters rwxrwxrwx are the "dummy permissions" of the symlink. All symlinks have the same apparent permissions, but their real permissions are those of the file they link to. A user who does not have permission to read a file is not able to read the file by reading a symlink to it (thankfully).
  - `b` block device (anything that can store information, hard drives etc), the files itself is a meeting file where kernel communicates with the hardware. Buffer on kernel, kerner stores bits of memory that the devices can access 
  - `c` character device (like mouse and keyboards), here it goes straight to the device. Device is responsible for buffering. 
  - `s` socket, communication channel visible to members of communication, "private file" 
  - `p` named pipe, almost never used, network sockets used instead 
- the rest are permissions 
  - 3 letters *owner* permission 
  - next 3 letters *group* permission 
  - next 3 letters *other* permission
  - r -read, w - write, x - executed (for directories can be entered)


*SCSI*
>> Small Computer System Interface (SCSI, /ˈskʌzi/ SKUZ-ee)[1] is a set of standards for physically connecting and transferring data between computers and peripheral devices. The SCSI standards define commands, protocols, electrical, optical and logical interfaces. The SCSI standard defines command sets for specific peripheral device types; the presence of "unknown" as one of these types means that in theory it can be used as an interface to almost any device, but the standard is highly pragmatic and addressed toward commercial requirements. The initial Parallel SCSI was most commonly used for hard disk drives and tape drives, but it can connect a wide range of other devices, including scanners and CD drives, although not all controllers can handle all devices. [wiki](https://en.wikipedia.org/wiki/SCSI)

- first drive usually `/dev/sda` (SATA) 
- on older systems first IDE hard drive `/dev/hda` (PATA)
- on newer systems, all IDE drives are named /dev/sda, /dev/sdb
- A master boot record (MBR) is a special type of boot sector at the very beginning of partitioned computer mass storage devices like fixed disks or removable drives intended for use with IBM PC-compatible systems and beyond. 
- The space on a hard drive is divided (or partitioned) into partitions. Partitions cannot overlap; space that is not allocated to a partition is called free space. The partitions have names like /dev/hda1, /dev/hda2, /dev/hda3, /dev/sda1, and so on. IDE drives are limited to 63 partitions on systems that do not use hotplug support for IDE drives. SCSI drives, USB drives, and IDE drives supported by hotplug are limited to 15 partitions [IBM Developer: Learn Linux, 101: Hard disk layout
](https://developer.ibm.com/tutorials/l-lpic1-102-1/)

- check nominal geometry on a Linux system using either `parted` or `fdisk`
- older Linux systems also reported geometry in the /proc filesystem, in a file such as /proc/ide/hda/geometry, a file that might not be present on newer systems.

**Disk management - partitions**
- MBR - master boot record (limited to 2TB)
- GPT - GUID (global unique identifier), 128 partitions, 9.4 ZB