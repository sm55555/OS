## ssh2 모듈 다운 시 에러

./configure --with-ssh2 --with-php-config=/usr/local/php/bin/php-config 명령 시

configure: WARNING: You will need re2c 0.13.4 or later if you want to regenerate PHP parsers.

```
wget https://sourceforge.net/projects/re2c/files/0.16/re2c-0.16.tar.gz
tar zxf re2c-0.16.tar.gz && cd re2c-0.16
./configure
make && make install
```

configure: error: The required libssh2 library was not found. You can obtain that package from....

```
yum install libssh2-devel
```
