## openssl 관련

```php
wget https://www.openssl.org/source/openssl-1.1.1i.tar.gz
tar xzf /root/tmp/openssl/openssl-1.1.1i.tar.gz
cd openssl-1.1.1i
./config --prefix=/opt/openssl-1.1.1i/bin -fPIC -shared
make -j 8 
make install

export PKG_CONFIG_PATH=/opt/openssl-1.1.1i/bin/lib/pkgconfig

```


https://stackoverflow.com/questions/50052339/compiling-php-7-2-with-openssl
