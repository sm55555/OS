## 방법 1

```
yum install zlib-devel
yum install gcc
wget --no-check-certificate https://www.openssl.org/source/openssl-1.1.1t.tar.gz
tar -zxvf openssl-1.1.1t.tar.gz
cd openssl-1.1.1t/


./config shared zlib
make && make install
cp /usr/local/lib64/libssl.so.1.1 /usr/lib64/libssl.so.1.1
cp /usr/local/lib64/libcrypto.so.1.1 /usr/lib64/libcrypto.so.1.1

echo "/usr/local/lib64/" >> /etc/ld.so.conf
ldconfig -v

ln -sf /usr/local/bin/openssl /bin
openssl version
```

## 방법 2
```
openssl 기존버젼 확인
openssl version

OpenSSL 1.0.2k-fips  26 Jan 2017

기존 openssl을 삭제
yum remove openssl

기본 라이브러리 설치
yum install gcc gcc-c++ pcre-devel zlib-devel perl wget
cd /usr/local/src
wget https://www.openssl.org/source/openssl-1.1.1g.tar.gz
tar xvfz openssl-1.1.1g.tar.gz
cd openssl-1.1.1g
./config --prefix=/usr/local/ssl --openssldir=/usr/local/ssl shared zlib

make & make install

만약 기존 openssl 1.0.2k 이 있다면 openssl 파일 변경
위에서 제거 했다면 생략
mv /bin/openssl /bin/openssl_1_0_2k

파일 생성 후 '/usr/local/ssl/lib' 내용 넣기

vi /etc/ld.so.conf.d/openssl-1.1.1g.conf
/usr/local/ssl/lib
ldconfig -v
ln -s /usr/local/ssl/lib/libssl.so.1.1 /usr/lib64/libssl.so.1.1
ln -s /usr/local/ssl/lib/libcrypto.so.1.1 /usr/lib64/libcrypto.so.1.1
ln -s /usr/local/ssl/bin/openssl /bin/openssl

openssl 버젼 확인

openssl version
OpenSSL 1.1.1g  21 Apr 2020

```

## 컴파일 프로그램 삭제 방법

```
./config 한 폴더 위치 가서
make uninstall

openssl version 체크
```
