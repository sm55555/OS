### 접근 제어

#### who : 현재사용한 접속자 출력 (복수 가능)

```
[user02@test_d log]$ who
ec2-user pts/0        2020-09-14 17:10 (211.206.114.80)
ec2-user pts/1        2020-09-15 14:50 (211.206.114.80)

```

#### whoami : 내 아이디 출력

```
[root@test_d security]# whoami
root
```



#### last : /var/log/wtmp 파일을 참고하여 로그인했던 정보를 출력해주는 명령어

```
[user02@test_d log]$ last
ec2-user pts/1        211.206.114.80   Tue Sep 15 14:50   still logged in   
ec2-user pts/0        211.206.114.80   Mon Sep 14 17:10   still logged in   
ec2-user pts/0        211.206.114.80   Mon Sep 14 09:52 - 12:54  (03:01)    
ec2-user pts/0        211.206.114.80   Fri Sep 11 17:28 - 17:35  (00:07)    
ec2-user pts/0        211.206.114.80   Tue Sep  8 15:23 - 15:41 (2+00:17)   
ec2-user pts/1        211.206.114.80   Wed Sep  2 15:49 - 10:17  (18:28)    
ec2-user pts/0        211.206.114.80   Wed Sep  2 09:17 - 10:17 (1+01:00)   
ec2-user pts/0        211.206.114.80   Mon Aug 24 08:35 - 15:07  (06:32)    
ec2-user pts/0        211.206.114.80   Fri Aug 21 16:37 - 08:24 (2+15:46)   
ec2-user pts/1        211.206.114.80   Fri Aug 21 15:36 - 15:53  (00:17)    

```
