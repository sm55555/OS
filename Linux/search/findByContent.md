# 파일속 내용으로 찾기

etc 하위 폴더를 대상으로 443이 포함된 파일 출력

```
grep -r "443" etc/*
```

/data/was/jbcs-2.4.37/httpd 하위에 "mod-jk"가 포함된 내용 출력

```
grep -r "mod-jk" /data/was/jbcs-2.4.37/httpd
```

현재 폴더 하위에 "7443"가 포함된 내용 출력

```
grep -r '7443' ./
```

특정 위치에  해당 콘텐츠를 가진 파일 이름 출력 ex) abcd

```
egrep -rl "abcd" /home/ec2-user/log


egrep -rl "abcd" /home/ec2-user/log | awk '{print " "$0" "}'
```

특정 위치에  해당 콘텐츠를 가진 파일 이름 출력하고 그 파일을 임의의 위치로 이동

```
egrep -rl "abcd" /home/ec2-user/log | awk '{print "cp "$0" /home/targetfolder/targetlog/"}'
```

