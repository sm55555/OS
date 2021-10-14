### 기본 상식

리눅스는 성능 향상을 위해 메모리 여유공간의 대부분을 캐시 영역으로 잡아둔다.

free 결과 

used는 5.9G이지만 buff/cache 영역에서 9.0G를 사용하기에 free 영역이 328M 밖에 없다.

```linux
[root@test ~]# free -h
              total        used        free      shared  buff/cache   available
Mem:            15G        5.9G        328M         81M        9.0G        9.0G
Swap:          8.0G        101M        7.9G
```

해당 서버 sar -1 결과

![image](https://user-images.githubusercontent.com/38831314/137234883-27ef0140-7670-4403-9d5c-5e3ac8b9ee2a.png)

사용률은 97% 이상으로 나온다.
