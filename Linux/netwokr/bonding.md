## bonding

리눅스의 여러 NIC를 논리적으로 묶는 것

```linux
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
