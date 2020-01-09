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


* * *


## Window

~~~

~~~
