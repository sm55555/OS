### python3.12 tar.gz 받은 후 압축풀기

컴파일하기 전 필요 사항

```
apt install gcc
apt-get install libc-dev 

```

설치를 위한 repo 구성

```
deb http://your-repository/ubuntu focal main restricted universe multiverse
deb http://your-repository/ubuntu  focal-updates main restricted universe multiverse
deb http://your-repository/ubuntu  focal-backports main restricted universe multiverse
deb http://your-repository/ubuntu  focal-security main restricted universe multiverse
deb http://your-repository/ubuntu  jammy main restricted universe multiverse
deb http://your-repository/ubuntu  jammy-updates main restricted universe multiverse
deb http://your-repository/ubuntu  jammy-backports main restricted universe multiverse
deb http://your-repository/ubuntu  jammy-security main restricted universe multiverse

```


```
cd /etc/Python-3.12.2
./configure --enable-optimizations
make -j$(nproc)
sudo make altinstall
```


```
python3.12 --version
```




