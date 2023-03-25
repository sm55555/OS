## ssh2 모듈 configure 시 에러

libssh2 관련 문제 있을 때

https://www.libssh2.org/download/ 에서 다운받자 나는	libssh2-1.9.0.tar.gz 이거 받음


## php.ini에 apuc.so

```
pecl install apcu
```

```
wget https://pecl.php.net/get/apcu-5.1.21.tgz
tar xvfz apcu-5.1.21.tgz
cd apcu-5.1.21.tgz
/usr/local/php/bin/phpize
./configure --with-php-config=/usr/local/php/bin/php-config
make
make install
```

## php.ini에 oci8.so 미인식 에러

```
pecl install oci8-2.2.0
```

pecl이 안될경우 따로 컴파일을 해줘야한다.

https://pecl.php.net/get/oci8-2.2.0.tgz22 에서 알맞은 PHP를 받은 다음

```
tar xvf oci8-2.2.0.tgz
cd oci8-2.2.0
/usr/local/php/bin/phpize
./configure --with-php-config=/usr/local/php/bin/php-config
make
make install
```

