# bonding

리눅스의 여러 NIC를 논리적으로 묶는 것

### NIC 확인

```
[root@localhost ~]# ifconfig
ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.91.128  netmask 255.255.255.0  broadcast 192.168.91.255
        inet6 fe80::20c:29ff:fe87:b70e  prefixlen 64  scopeid 0x20<link>
        ether 00:0c:29:87:b7:0e  txqueuelen 1000  (Ethernet)
        RX packets 226  bytes 22388 (21.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 172  bytes 26838 (26.2 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

ens36: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.91.129  netmask 255.255.255.0  broadcast 192.168.91.255
        inet6 fe80::20c:29ff:fe87:b718  prefixlen 64  scopeid 0x20<link>
        ether 00:0c:29:87:b7:18  txqueuelen 1000  (Ethernet)
        RX packets 9  bytes 1104 (1.0 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 22  bytes 2236 (2.1 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 10  bytes 1010 (1010.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 10  bytes 1010 (1010.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

[root@localhost ~]#
```

### 네트워크 환경 설정 변경

```
[root@localhost network-scripts]# cd /etc/sysconfig/network-scripts/
[root@localhost network-scripts]#
```

```
[root@localhost network-scripts]# vi ifcfg-ens33
BOOTPROTO=none
NAME=ens33
DEVICE=ens33
ONBOOT=yes
MASTER=bond0
SLAVE=yes

[root@localhost network-scripts]# vi ifcfg-ens36
BOOTPROTO=dhcp
NAME=ens36
DEVICE=ens36
ONBOOT=yes
MASTER=bond0
SLAVE=yes
[root@localhost network-scripts]#
```

### 본딩 파일 생성

```
[root@localhost network-scripts]# vi ifcfg-bond0
BOOTPROTO=none
NAME=bond0
DEVICE=bond0
ONBOOT=yes
TYPE=Bond
IPADDR=192.168.91.110
NETMASK=255.255.255.0
GATEWAY=192.168.91.2
BONDING_OPTS=mode=1 miimon=10 primary=ens33 fail_over_mac=1
[root@localhost network-scripts]#
```

### 본딩 모듈 적재

```
[root@localhost network-scripts]# modprobe --first-time bonding
[root@localhost network-scripts]#
```

### 본딩 설정 적용 및 확인

```
[root@localhost ~]# systemctl restart network
[root@localhost ~]#
```

### Bonding의 세부설정을 확인

```
[root@localhost ~]# cat /proc/net/bonding/bond0
Ethernet Channel Bonding Driver: v3.7.1 (April 27, 2011)

Bonding Mode: fault-tolerance (active-backup) (fail_over_mac active)
Primary Slave: ens33 (primary_reselect always)
Currently Active Slave: ens33
MII Status: up
MII Polling Interval (ms): 10
Up Delay (ms): 0
Down Delay (ms): 0

Slave Interface: ens33
MII Status: up
Speed: 1000 Mbps
Duplex: full
Link Failure Count: 0
Permanent HW addr: 00:0c:29:87:b7:0e
Slave queue ID: 0

Slave Interface: ens36
MII Status: up
Speed: 1000 Mbps
Duplex: full
Link Failure Count: 0
Permanent HW addr: 00:0c:29:87:b7:18
Slave queue ID: 0
[root@localhost ~]#
```



