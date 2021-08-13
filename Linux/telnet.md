### 방화벽이 오픈되어 있고 프로세스가 떠 있는 경우

```cmd
[root@192.168.10.20]# telnet 192.168.10.21 22
Trying 192.168.10.21...
Connected to 192.168.10.21 (192.168.10.21).
Escape character is '^]'.
SSH-2.0-OpenSSH_4.3
```

### 방화벽만 오픈되어 있고 프로세스가 꺼져있는 경우

```cmd
[root@192.168.10.20]# telnet 192.168.10.21 4080
Trying 192.168.10.21... 바로 뜸
telnet: connect to address 192.168.10.20: Connection refused
telnet: Unable to connect to remote host: Connection refused
```

### 방화벽이 닫혀 있는 경우

```cmd
[root@192.168.10.20]# telnet 192.168.10.21 5443
Trying 192.168.10.21... 딜레이 계속됨
telnet: connect to address 192.168.10.21: Connection timed out
telnet: Unable to connect to remote host: Connection timed out
```

### 타겟 위치에 실행되고 있는 프로세스들을 확인해보자

```cmd
[root@192.168.10.20]$ ps -ef | grep 22
root      2292     2  0 May26 ?        00:00:00 [ena]
root      2296     1  0 May26 ?        00:00:00 /usr/lib/systemd/systemd-udevd
root      3136     1  0 May26 ttyS0    00:00:00 /sbin/agetty --keep-baud 115200,38400,9600 ttyS0 vt220
```
