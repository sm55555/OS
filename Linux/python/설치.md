
### wget 으로 Python-3.12.2.tgz 다운

Amazon linux 2023 환경

```
[root@test ~]# yum groupinstall "Developments Tools"
```

```
[root@test ~]# tar -xzvf Python-3.12.2.tgz
[root@test ~]# cd /etc/Python-3.12.2

[root@test ~]# ./configure --enable --optimizations
[root@test ~]# make -j$(nproc)
[root@test ~]# make install

[root@test ~]# python3.12 --verison
```

### 모든 계정 다 넣고 싶으면 


/etc/bashrc

```
alias python='/usr/local/bin/python3.12'
```
