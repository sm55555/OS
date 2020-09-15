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



#### last : /var/log/wtmp 파일을 참고하여 로그인했던 정보를 출력해주는 명령어 및 시스템 부팅 기록 확인

```
[user02@test_d log]$ last
ec2-user pts/1        211.206.114.80   Fri Aug 21 15:36 - 15:53  (00:17)    
ec2-user pts/0        211.206.114.80   Fri Aug 21 13:16 - 15:53  (02:36)    
ec2-user pts/0        211.206.114.80   Thu Aug 20 12:52 - 09:37  (20:44)    
reboot   system boot  4.14.186-146.268 Thu Aug 20 12:41 - 14:54 (26+02:13)  
ec2-user pts/0        211.206.114.80   Thu Aug 20 08:39 - 09:26  (00:47)    
reboot   system boot  4.14.186-146.268 Wed Aug 19 15:58 - 10:56  (18:57)    
ec2-user pts/0        211.206.114.80   Wed Aug 19 15:21 - 15:47  (00:26)    
reboot   system boot  4.14.186-146.268 Wed Aug 19 15:20 - 10:56  (19:36)    
ec2-user pts/0        211.206.114.80   Wed Aug 19 11:00 - 15:12  (04:11)    
ec2-user pts/0        211.206.114.80   Tue Aug 18 16:20 - 17:36  (01:16)    
ec2-user pts/0        211.206.114.80   Tue Aug 11 13:40 - 17:00  (03:20)    
ec2-user pts/0        211.206.114.80   Mon Aug 10 14:38 - 11:07  (20:28)    
reboot   system boot  4.14.186-146.268 Mon Aug 10 14:35 - 15:12 (9+00:36)   


```
