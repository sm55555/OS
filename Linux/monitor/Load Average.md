## Load Average 란

```
프로세스의 여러 상태 중 R 또는 D 상태에 있느 프로세스들의 개수르 1분, 5분, 15분 단위로 평균 값을 나타낸것이다.
Load Average는 코어의 값에 따라 상대적이다. 코어 4개에서 Load Average 8은 코어 4개가 각각 동시에 작동하므로 2에 가까우며,
코어 1개 Load Average 8은 한 번에 하나만 실행하게 되므로 8을 나타낸다.
```

##### R

R: Running 상태로써 프로세스가 실제로 CPU 자원을 소모하고 있는 실행 중인 상태이다. R이 많다는 것은 CPU 리소르 측면에서 부하가 있다는 것으로 판단할 수 있다.

##### D

D: Uninterruptible Sleep 상태로써 인터럽트에 의해서 상태가 변경되지 않는 대기 상태이다. 보통 디스크 또는 네트워크 I/O 작업 처리를 대기 중인 프로세스의 상태를 말한다.

### Load Average 확인 방법

```
[root@ ~]# uptime
13:45:39 up 31 min,  2 users,  load average: 0.00, 0.00, 0.03
```

### Load Average 높아졌을 때 어떻게 해야 할까?

R 상태의 프로세스의 개수가 많아서인지 또는 D 상태의 프로세스가 많아서 인지 구분해야한다.
R의 상태는 실행 중인 프로세스로 CPU 리소스를 사용 중인 상태라고 했다. 즉 CPU 리소스 부하를 의미한다.
D의 상태는 네트워크 또는 디스크의 응답을 대기하는 상태 즉, I/O 부하를 의미한다.

## vmstat (Virtual Memory Statics)은 현재 메모리 및 CPU의 사용률을 알 수 있는 툴이다.

```
[root@ ~]# vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 0  0      0 504328   2088 342004    0    0  9076   243  512 3103 36 10 26  1 26
```

r은 실행되기를 기다리거나 실행 중인 프로세스의 개수를 나타내며, b는 uninterruptible sleep 상태의 프로세스로 I/O를 위해 대기열에 있는
프로세스의 개수를 나타낸다. 그러므로 r은 R 상태의 프로세스 개수이며 b는 D 상태의 프로세스 개수를 나타낸다.

즉, Load Average가 높아졌을때 Vmstat을 통해 CPU 리소스 부하(R) 떄문인지 I/O 부하(D) 때문인지 원인 파악이 가능하다.









