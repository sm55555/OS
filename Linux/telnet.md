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
