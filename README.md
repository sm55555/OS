# Command

## Linux

enviroment : amazon linux2 (centOS)


### netstat

~~~

[ec2-user@ip-10-0-0-86 ~]$ netstat -anp
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      -                   
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      -                   
tcp        0    416 10.0.0.86:22            211.206.114.80:41251    ESTABLISHED -                   
tcp6       0      0 :::111                  :::*                    LISTEN      -                   
tcp6       0      0 :::22                   :::*                    LISTEN      -                   
udp        0      0 0.0.0.0:753             0.0.0.0:*                           -                   
udp        0      0 127.0.0.1:323           0.0.0.0:*                           -                   
udp        0      0 0.0.0.0:68              0.0.0.0:*                           -                   
udp        0      0 0.0.0.0:111             0.0.0.0:*                           -   
...

~~~

netstat shows the communication status of the network interface installed on the host

### find 

~~~

sudo find / -name "*aaaaa*"

~~~
It prints the files that contain the corresponding input

You have to wirte "sudo" because linux find command is search from root directory

### dig

~~~

[ec2-user@ip-10-0-0-86 ~]$ dig naver.com +trace
; <<>> DiG 9.11.4-P2-RedHat-9.11.4-9.P2.amzn2.0.2 <<>> nave.com +trace
;; global options: +cmd
.			518400	IN	NS	G.ROOT-SERVERS.NET.
.			518400	IN	NS	H.ROOT-SERVERS.NET.
.			518400	IN	NS	I.ROOT-SERVERS.NET.
.			518400	IN	NS	J.ROOT-SERVERS.NET.
.			518400	IN	NS	K.ROOT-SERVERS.NET.
.			518400	IN	NS	L.ROOT-SERVERS.NET.
.			518400	IN	NS	M.ROOT-SERVERS.NET.
.			518400	IN	NS	A.ROOT-SERVERS.NET.
.			518400	IN	NS	B.ROOT-SERVERS.NET.
.			518400	IN	NS	C.ROOT-SERVERS.NET.
.			518400	IN	NS	D.ROOT-SERVERS.NET.
.			518400	IN	NS	E.ROOT-SERVERS.NET.
.			518400	IN	NS	F.ROOT-SERVERS.NET.
;; Received 239 bytes from 10.0.0.2#53(10.0.0.2) in 0 ms
...

~~~

dig shows the information (IP Address and domain) through the Name Server

### nslookup

~~~

[ec2-user@ip-10-0-0-86 ~]$ nslookup naver.com
Server:		10.0.0.2
Address:	10.0.0.2#53

Non-authoritative answer:
Name:	naver.com
Address: 210.89.160.88
Name:	naver.com
Address: 210.89.164.90
Name:	naver.com
Address: 125.209.222.141
Name:	naver.com
Address: 125.209.222.142

[ec2-user@ip-10-0-0-86 ~]$ nslookup -type=ns naver.com
Server:		10.0.0.2
Address:	10.0.0.2#53

Non-authoritative answer:
naver.com	nameserver = ns1.naver.com.
naver.com	nameserver = ns2.naver.com.

Authoritative answers can be found from:

[ec2-user@ip-10-0-0-86 ~]$ nslookup naver.com ns1.naver.com
Server:		ns1.naver.com
Address:	125.209.248.6#53

Name:	naver.com
Address: 210.89.160.88
Name:	naver.com
Address: 125.209.222.141
Name:	naver.com
Address: 210.89.164.90
Name:	naver.com
Address: 125.209.222.142

~~~

nslookup shows the information(IP Address and domain) through the Name Server

* nslookup -type=ns [domain]

shows DNS name

* nslookup [domain] [DNS name]

shows the information (IP Address and domain) as an administrator

### route

~~~

[ec2-user@ip-10-0-0-86 ~]$ route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         ip-10-0-0-1.ap- 0.0.0.0         UG    0      0        0 eth0
10.0.0.0        0.0.0.0         255.255.255.0   U     0      0        0 eth0
instance-data.a 0.0.0.0         255.255.255.255 UH    0      0        0 eth0
[ec2-user@ip-10-0-0-86 ~]$ netstat -r
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
default         ip-10-0-0-1.ap- 0.0.0.0         UG        0 0          0 eth0
10.0.0.0        0.0.0.0         255.255.255.0   U         0 0          0 eth0
instance-data.a 0.0.0.0         255.255.255.255 UH        0 0          0 eth0

~~~

route is show information about default gateway

* In Windows, the ipconfig command shows default gateway, But Linux ifconfig does not show default gateway

### ip addr && ifconfig

~~~

[ec2-user@ip-10-0-0-86 ~]$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 02:ca:05:a7:e5:58 brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.86/24 brd 10.0.0.255 scope global dynamic eth0
       valid_lft 2403sec preferred_lft 2403sec
    inet6 fe80::ca:5ff:fea7:e558/64 scope link 
       valid_lft forever preferred_lft forever
       
       
[ec2-user@ip-10-0-0-86 ~]$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 10.0.0.86  netmask 255.255.255.0  broadcast 10.0.0.255
        inet6 fe80::ca:5ff:fea7:e558  prefixlen 64  scopeid 0x20<link>
        ether 02:ca:05:a7:e5:58  txqueuelen 1000  (Ethernet)
        RX packets 34300  bytes 39989237 (38.1 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 6771  bytes 780359 (762.0 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 36  bytes 1740 (1.6 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 36  bytes 1740 (1.6 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

~~~

* ip addr and ifconfig show the information about ip and another setting
* The ifconfig command does not show the information set in Network Manager


du <--- about disk

* * *


## Window

~~~

ncpa.cpl

~~~
