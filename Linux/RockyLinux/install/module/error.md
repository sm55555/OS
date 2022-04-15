## PHP-m 모듈 문제 시

모듈 설치 위치에서 아래 명령어를 통해 확인할 수 있다.

```
ldd oci8.so

....
libnsl.so.1 => Not Found
...

```

위와 같은 메세지가 뜬다.

https://web-obj.tistory.com/328

```
yum install -y libnsl
또는
pecl install apcu
```

위 처럼 해결 할 수 있지만 안되는것도 있다. 

ex) libmcrypt.so.4 => Not Found

https://rpmfind.net/linux/epel/8/Everything/x86_64/Packages/l/libmcrypt-2.5.8-26.el8.x86_64.rpm2

## ssh2 모듈 configure 시 에러

libssh2 관련 문제 있을 때

https://www.libssh2.org/download/ 에서 다운받자 나는	libssh2-1.9.0.tar.gz 이거 받음


## php.ini에 apuc.so

```
pecl install apcu
```

## php.ini에 oci8.so 미인식 에러

```
pecl install oci8-2.2.0
```
