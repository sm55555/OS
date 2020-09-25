### fdisk 용량 추가 방법

사용환경 : 아마존리눅스2

1. voulume 추가 및 attach (여기선 2GB추가 == 2048MB 사용 가능)

2. 예시는 3번 째 파티션 추가 시

```
[root@test_d pkginstall]# fdisk /dev/xvdf

Welcome to fdisk (util-linux 2.30.2).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


Command (m for help): n
Partition type
   p   primary (2 primary, 0 extended, 2 free)
   e   extended (container for logical partitions)
Select (default p): 

Using default response p.
Partition number (3,4, default 3): 
First sector (616448-4194303, default 616448): 
Last sector, +sectors or +size{K,M,G,T,P} (616448-4194303, default 4194303): +150M

Created a new partition 3 of type 'Linux' and of size 150 MiB.

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

[root@test_d pkginstall]# fdisk -l
Disk /dev/xvda: 8 GiB, 8589934592 bytes, 16777216 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 24F84068-53BE-4AE2-A53D-CBAC5515B1AF

Device       Start      End  Sectors Size Type
/dev/xvda1    4096 16777182 16773087   8G Linux filesystem
/dev/xvda128  2048     4095     2048   1M BIOS boot

Partition table entries are not in disk order.


Disk /dev/xvdf: 2 GiB, 2147483648 bytes, 4194304 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x863a94e3

Device     Boot  Start    End Sectors  Size Id Type
/dev/xvdf1        2048 206847  204800  100M 83 Linux
/dev/xvdf2      206848 616447  409600  200M 83 Linux
/dev/xvdf3      616448 923647  307200  150M 83 Linux
[root@test_d pkginstall]# fdisk /dev/xvdf
```

#### Primary Partion은 4개만 사용 가능

MBR 파티션 관련이 64바이트고 Primary Partion 당 16 바이트가 필요해서 4개만 생성 가능

```
Command (m for help): n
To create more partitions, first replace a primary with an extended partition.
```

#### 파티션 5개 이상 사용법

하나의 Primary Partion 지우고 Extended Partiion 추가

!! Extended Partiion 추가 시 용량을 전부다 할당한다 -> 그 다음 생성 때부터 용량 설정 가능

```
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


Command (m for help): n
Partition type
   p   primary (3 primary, 0 extended, 1 free)
   e   extended (container for logical partitions)
Select (default e): e

Selected partition 4
First sector (923648-4194303, default 923648): 
Last sector, +sectors or +size{K,M,G,T,P} (923648-4194303, default 4194303): 

Created a new partition 4 of type 'Extended' and of size 1.6 GiB.

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

[root@test_d pkginstall]# fdisk -l
Disk /dev/xvda: 8 GiB, 8589934592 bytes, 16777216 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 24F84068-53BE-4AE2-A53D-CBAC5515B1AF

Device       Start      End  Sectors Size Type
/dev/xvda1    4096 16777182 16773087   8G Linux filesystem
/dev/xvda128  2048     4095     2048   1M BIOS boot

Partition table entries are not in disk order.


Disk /dev/xvdf: 2 GiB, 2147483648 bytes, 4194304 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x863a94e3

Device     Boot  Start     End Sectors  Size Id Type
/dev/xvdf1        2048  206847  204800  100M 83 Linux
/dev/xvdf2      206848  616447  409600  200M 83 Linux
/dev/xvdf3      616448  923647  307200  150M 83 Linux
/dev/xvdf4      923648 4194303 3270656  1.6G  5 Extended
[root@test_d pkginstall]# fdisk /dev/xvdf

Welcome to fdisk (util-linux 2.30.2).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


Command (m for help): n
All primary partitions are in use.
Adding logical partition 5
First sector (925696-4194303, default 925696): 
Last sector, +sectors or +size{K,M,G,T,P} (925696-4194303, default 4194303): +250M

Created a new partition 5 of type 'Linux' and of size 250 MiB.

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

[root@test_d pkginstall]# fdisk -

Welcome to fdisk (util-linux 2.30.2).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

fdisk: cannot open -: No such file or directory
[root@test_d pkginstall]# fdisk -l
Disk /dev/xvda: 8 GiB, 8589934592 bytes, 16777216 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 24F84068-53BE-4AE2-A53D-CBAC5515B1AF

Device       Start      End  Sectors Size Type
/dev/xvda1    4096 16777182 16773087   8G Linux filesystem
/dev/xvda128  2048     4095     2048   1M BIOS boot

Partition table entries are not in disk order.


Disk /dev/xvdf: 2 GiB, 2147483648 bytes, 4194304 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x863a94e3

Device     Boot  Start     End Sectors  Size Id Type
/dev/xvdf1        2048  206847  204800  100M 83 Linux
/dev/xvdf2      206848  616447  409600  200M 83 Linux
/dev/xvdf3      616448  923647  307200  150M 83 Linux
/dev/xvdf4      923648 4194303 3270656  1.6G  5 Extended
/dev/xvdf5      925696 1437695  512000  250M 83 Linux
[root@test_d pkginstall]# fdisk /dev/xvdf

```



