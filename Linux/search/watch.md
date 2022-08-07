# watch

watch 명령은 원하는 명령어의 결과를 원하는 시간(초) 주기로 리프레시 하여 결과를 보여주는 명령어 입니다.

```
[root@localhost]# watch [-d] [-n seconds] 'command'
```

#### Apache 5초간 모니터링

```
[root@localhost]# watch -n 5 'ps -ef | grep httpd'
```
