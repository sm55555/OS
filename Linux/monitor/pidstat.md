## pidstat

PID 기반으로 사용률 조회

##### 해당 PID CPU 사용량 출력 

```
pidstat -l -p 3003
pidstat -l -p [ALL]
```

##### 해당 PID 메모리 출력 

```
pidstat -r -p 3003
pidstat -r -p [ALL]
```

##### 해당 PID DISK IO 출력

```
pidstat -d -p 3003
pidstat -d -p [ALL]
```
