## disabled ThreadSaftey in Rocky linux

```
/usr/local/php/bin/php -i | grep -i thread

Thread Safety -> Enabled
```

#### 1. Apache를 설치한 다음 prefork 형식으로 바꾸어주고 기동을한다.

```
vi /etc/httpd/conf.modules.d/00-mpm.conf에서 아래내용만 주석 해체 하고 실행 

LoadModule mpm_prefork_module modules/mod_mpm_prefork.so
```

확인 

```
httpd -V | grep MPM
```

#### 2. PHP 설치 위치에서 configure 수정

ex) /usr/local/src/php-7.2.10/configure

```
#APXS_MPMM=`$APXS -q MPM NAME`을 아래 처럼 바꾼다.
APXS _MPM=`httpd -V|awk '\^Server MPM\{print $3}`
```

#### 컴파일 진행

```
/usr/local/php/bin/php -i | grep -i thread

Thread Safety -> Disabled 확인

```


