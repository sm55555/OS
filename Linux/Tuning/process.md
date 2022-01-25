# 리눅스 커널 파라미터를 튜닝하여 동시 처리량 늘리기

- fs.file-max 모든 프로세스의 대해 열린 파일의 최대 수를 지정합니다.

```
[fs.file-max 수정]

# echo "fs.file-max=65535" >> /etc/sysctl.conf
# sysctl -a
```

[/etc/security/limits.conf 수정]

```
nginx hard nproc 10240
nginx soft nproc 10240
nginx hard nofile 204800
nginx soft nofile 204800
```
