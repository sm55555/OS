## 생성 날짜로 찾기

```
find . -name "*.gz" -mtime +60
```

.gz으로 끝나는 파일 중 60일 이상 된것들을 출력해라 

```
[root@ ~] find . -name "*.gz" -mtime +60
./error.log-20201011.gz
./error.log-20201012.gz
./error.log-20201013.gz
./error.log-20201014.gz
./error.log-20201015.gz
```
