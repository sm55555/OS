## SwapMemory

SwapMemory

시스템에 메모리가 부족할 경우에 하드디스크의 일부 공간을 활용하여 계속 작업을 도와주는 영역 (메모리 공간 부족 방지를 위한 임시 방편)
-> 하드디스크의 일부를 RAM처럼 사용할 수 있게 만드는 것

#### 확인 방법

Swap 부분이 0이면 없어짐

```
[root@test ~]# free -g
              total        used        free      shared  buff/cache   available
Mem:             30           8           0           0          21          22
Swap:             0           0           0
```

아래 명렁어를 치고 아무것도 없으면 없음

```
swapon -s
```

#### SwapMemory 설정 방법

ex) /swapfile

```
chmod 600 /swapfile
dd if=/dev/zero of=/swapfile bs=1MiB count=8192 (1024가 1GB)
mkswap /swapfile
swapon /swapfile
```

#### SwapMemory 해체 방법

```
swapoff /swapfile 
```

#### SwapMemory 리부팅 후에도 설정 방법

vi /etc/fstab

```
/swapfile swap swap defaults 0 0
```
