### 파일 소유자 관련

/test 폴더만 소유자 : appadmin, 소유 그룹 : app 으로 변경

```
chown appadmin:app /test
```

/test 및 하위 모든 파일 소유자 : appadmin, 소유 그룹 : app 으로 변경

```
chown -R appadmin:app /test
```

### 파일 권한 관련

rwxrwxrwx

```
chmod 777 test.txt
```

other에 execute 권한할당

```
chmod o+x test.txt
```

### 주체 정보

u : 소유자
g : 그룹
o : other

r : read
w : write
x : execute(실행)


