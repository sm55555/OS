## lvm create

```
/dev/xvdf 
3GB
/dev/xvdg
5GB

4GB 4 GB 해보자

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

/dev/myVG/myLG1                    /lvm1        ext4    defaults          0   0
/dev/mapper/vg_data-lv_logs                   /logs       ext4    defaults          0   0

```
