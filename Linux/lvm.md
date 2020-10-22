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

### 할당하는게 2GB 이상 이면 다르게 해야함

```

- 2TB이상에서는 GPT볼륨으로 구성을 해야 하는데 fdisk 로는 파티션을 잡을 수 없다.. 
그래서 parted 로 설정을 해야함. 

# fdisk -l 로 현재 장치명 확인 
/dev/sdb  /dev/sdc  다른 디스크가 없다면 이렇게 보일 것 임.
# parted /dev/sdb
<parted> mklabel gpt
<parted> unit gb or unit tb  : 사용 단위 지정
<parted> mkpart primary 0 100% : 용량을 4096GB로 설정해도 됨
<parted> set 1 lvm on : lvm으로 설정을 할 것 이기 때문에
<parted> print : 잘 잡혔는지 확인
<parted> q       : 빠져 나옴
# parted /dev/sdc : 이것도 동일하게 설정
# fdisk -l로 다시 확인 
/dev/sdb1 /dev/sdc1 으로 파티션이 설정된 것이 보임


-> 그 후 LVM 생성

```

