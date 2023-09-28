### logdelete

기본적으로 find는 하위까지 다 보지만 depth를 이용하여 깊이를 조절할 수 있다.

/var/log에 만 있는 *.gz 이름을 가진 로그 지우기

```
find /var/log -maxdepth 1 -name *.gz -delete
```

/home 폴더 및 하위 모든 .log 파일 삭제

```
find /home/ -name *.log -delete
```
