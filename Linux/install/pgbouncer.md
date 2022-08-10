
# [pgbouncer 설치]


### openssl 변경 -> git 참고
https://github.com/sm55555/OS/blob/master/Linux/openssl/version%20change.md

```
wget https://www.openssl.org/source/openssl-1.1.1q.tar.gz
```
### pgbouncer 컴파일 설치

```
wget https://www.pgbouncer.org/downloads/files/1.17.0/pgbouncer-1.17.0.tar.gz
/configure --prefix=/usr/local
```

### libevent 컴파일 설치

```
yum install libevent-devel
wget https://github.com/libevent/libevent/releases/download/release-2.1.12-stable/libevent-2.1.12-stable.tar.gz
/configure --prefix=/usr/local
```
