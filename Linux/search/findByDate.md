## 생성 날짜로 찾기

.gz으로 끝나는 파일 중 60일 이상 된것들을 출력해라 
```
find . -name "*.gz" -mtime +60
```
```
[root@ ~] find . -name "*.gz" -mtime +60
./error.log-20201011.gz
./error.log-20201012.gz
./error.log-20201013.gz
./error.log-20201014.gz
./error.log-20201015.gz
```
.gz으로 끝나는 파일 중 60일 이상 된것들을 삭제해라 
```
find . -name "*.gz" -mtime +60 -delete
```
갯수 출력
```
[root@ ~] find . -name "*.gz" | wc -l
37
```
