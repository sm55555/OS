## inode 관련

inode : 파일을 기술하는 디스크 상의 데이터 구조로서 파일의 데이터 블록이 디스크 상의 어느 주소에 위치하고 있는가와 같은 파일에 대한 중요한 정보를 갖고 있다.
 
inode 확인 방법

df -i : IUse% 확인
```cmd
[root@ip-111-11-1-11 ~]# df -i
Filesystem      Inodes IUsed   IFree IUse% Mounted on
devtmpfs        123169   284  122885    1% /dev
tmpfs           125861     2  125859    1% /dev/shm
tmpfs           125861   361  125500    1% /run
tmpfs           125861    16  125845    1% /sys/fs/cgroup
/dev/xvda1     4193216 60036 4133180    2% /
tmpfs           125861     1  125860    1% /run/user/1000
```


