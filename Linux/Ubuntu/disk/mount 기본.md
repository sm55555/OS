### mount more thatn volume 2TB

mount에 필요한 disk 있는지 먼저 확인

```
fdisk -l
```

Output:
```
parted /dev/sdb
GNU Parted 2.3
Using /dev/sdb
Welcome to GNU Parted! Type 'help' to view a list of commands.
```


Output:
```
(parted) mklabel gpt
```

Output:
```
Warning: The existing disk label on /dev/sdb will be destroyed and all data on this disk will be lost. Do you want to continue?
Yes/No? yes
(parted)
```

Output
```
(parted) unit TB
```

Output
```
(parted) mkpart primary 0.00TB 3.00TB
```

Output
```
(parted) print
```

Output
```
Model: ATA ST33000651AS (scsi)
Disk /dev/sdb: 3.00TB
Sector size (logical/physical): 512B/512B
Partition Table: gpt

Number  Start   End     Size    File system  Name     Flags
 1      0.00TB  24.00TB  24.00TB  ext4         primary
```

Output
```
(parted) quit
```

Output
```
mkfs.ext4 /dev/sdb
```





https://www.cyberciti.biz/tips/fdisk-unable-to-create-partition-greater-2tb.html
