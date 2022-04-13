## ssh2 모듈 configure 시 에러

```
[root@localhost ~] ./configure --with-ssh2 --with-php-config=/usr/local/php/bin/php-config 명령 시
```

configure: WARNING: You will need re2c 0.13.4 or later if you want to regenerate PHP parsers.

```
[root@localhost ~] wget https://sourceforge.net/projects/re2c/files/0.16/re2c-0.16.tar.gz
[root@localhost ~] tar zxf re2c-0.16.tar.gz && cd re2c-0.16
[root@localhost ~] ./configure
[root@localhost ~] make && make install
```

configure: error: The required libssh2 library was not found. You can obtain that package from....

```
[root@localhost ~] yum install libssh2-devel
```
