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


## openssl configure 시 에러

https://stackoverflow.com/questions/50052339/compiling-php-7-2-with-openssl

나의 경우 php 7.2가 테스트였다.

### 1.Install OpenSSL

```
wget https://www.openssl.org/source/openssl-1.1.1i.tar.gz
tar xzf /root/tmp/openssl/openssl-1.1.1i.tar.gz
cd openssl-1.1.1i
./Configure --prefix=/opt/openssl-1.1.1i/bin -fPIC -shared linux-x86_64
make -j 8 
make install
```

2.Export the variable PKG_CONFIG_PATH to point to pkgconfig directory

```
export PKG_CONFIG_PATH=/opt/openssl-1.1.1i/bin/lib/pkgconfig
```

3. recompile

