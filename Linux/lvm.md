## lvm create


### 3GB 5GB EBS에서 추가 - > free tier시 30GB까지 무료,,,

```
/dev/xvdf 
3GB
/dev/xvdg
5GB

```

### 4GB 4 GB 해보자

```
pvcreate /dev/xvdf1
pvcreate /dev/xvdg1

vgcreate myVG /dev/xvdf1 /dev/xvdg1

lvcreate --size 4G --name myLG1 myVG
lvcreate --extents 100%FREE --name myLG2 myVG


mkfs.ext4 /dev/myVG/myLG1
mkfs.ext4 /dev/myVG/myLG2

mkdir /lvm1 /lvm2

mount /dev/myVG/myLG1 /lvm1
mount /dev/myVG/myLG2 /lvm2


vi /etc/fstab

/dev/myVG/myLG2                    /lvm2        ext4    defaults          0   0
/dev/myVG/myLG1                    /lvm1        ext4    defaults          0   0

```

### 축소 -> 백업 반드시 필요 

```
umount /lvm1

e2fsck -f /dev/myVG/myLG1
resize2fs /dev/myVG/myLG1 1G
lvreduce -L -3G /dev/myVG/myLG1

y 누름

mount /dev/myVG/myLG1 /lvm1
df -h
```

### 증가

```
lvextend -L4G /dev/myVG/myLG1
resize2fs /dev/myVG/myLG1 
```

### LVM 삭제 방법

```
umount /lvm1
umount /lvm2

lvremove /dev/myVG/myLG1
lvremove /dev/myVG/myLG2

vgremove myVG

pvdisplay (이름이 변경 되어서 확인하고 지워야함) 
df -Th

pvremove /dev/xvdf1
pvremove /dev/xvdg1
```
