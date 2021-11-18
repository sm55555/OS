### disk i/o 이슈 시

disk i/o 높은 경우

![image](https://user-images.githubusercontent.com/38831314/142376103-d7707220-2f5c-4868-879b-0f2afd7d0598.png)

##### 아래 명령어로 disk i/o 사용 프로세스 확인 가능

```
pidstat -d -p ALL
pidstat -d -p [PID]
```

```
Linux 3.10.0-1160.36.2.el7.x86_64 (was1) 	11/18/2021 	_x86_64_	(4 CPU)

05:11:04 PM   UID       PID   kB_rd/s   kB_wr/s kB_ccwr/s  Command
05:11:04 PM     0         1      0.00      0.00      0.00  systemd
05:11:04 PM     0         2      0.00      0.00      0.00  kthreadd
```

확인해보니 gp2를 사용하느 EBS가 Burst를 다 소진하여 i/o가 부족현상 발생(0이 되는게 Burst를 다 소진)

##### 해당 EBS -> monitor 탭 -> Burst balance (%)

![image](https://user-images.githubusercontent.com/38831314/142376649-962ffced-2708-45aa-be8e-7323433040c0.png)

gp3로 타입 변경해서 해결 (타입 변경은 서비스에 영향이 없다.)
