# alias

1. go to home directory

```
[root@test_d ~]# vi .bashrc

alias vi='vim' 
```

### after modify

```
[root@test_d ~]# source .bashrc
```

#### 모든 계정에 Alias 적용

```
vi /etc/bashrc/

가장 밑에

alias python='/usr/local/bin/python3.12'
```

#### 적용 및 확인
```
source /etc/bashrc

pytonh --version
```

