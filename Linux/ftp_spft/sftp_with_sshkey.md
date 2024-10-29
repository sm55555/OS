
## source server

소스 서버 해당 접속할 유저에서 key 생성

```
ssh-keygen -t rsa
```

pulbic key 값 복사

```
cat ~/.ssh/id_rsa.pub 
```


## target server

예를들어 test-ftp 유저가 있다. (nologin), 홈폴더는 /data 인 경우
/data/test 에 파일을 쌓아야한다.

/data root:root 로 잡는다.

```
/data
```

```
chown root:root /data
chown 755 /data
```


해당 홈 폴더(/data)에서 하위 폴더를 만든다.
.ssh/authorized_keys  -> 다음에 .ssh/authorized_keys  pulbic key 값 복사을 넣는다.


#### /etc/ssh/sshd_config 설정

```
Match User fss2
        ChrootDirectory /data
        ForceCommand internal-sftp
        AllowTcpForwarding no
        X11Forwarding no
```



