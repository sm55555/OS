# sftp 끄는법 (cent os 7)


etc/ssh/sshd_config 파일열기

```
$ vi /etc/ssh/sshd_config
```

아래와 같이 Subsystem 항목을 주석처리를 해준후 저장

```
# Subsystem      sftp    /usr/libexec/openssh/sftp-server
```

ssh 재시작

```
$ systemctl restart sshd
```
