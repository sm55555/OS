# 파일속 내용으로 찾기

etc 하위 폴더를 대상으로 443이 포함된 파일 출력

```
grep -r "443" etc/*
```

/data/was/jbcs-2.4.37/httpd 하위에 "mod-jk"가 포함된 내용 출력

```
grep -r "mod-jk" /data/was/jbcs-2.4.37/httpd
```
