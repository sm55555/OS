## mount

```
mount -t cifs //smfile01.sss.com/storage/ /was/test -o username=osm,password=12345,domain=test.co.kr,uid=1003,gid=1003
```

설명 -> 공유 스토리지인 //smfile01.sss.com/storage/에 접속 시도하려고한다.

계정은 AD 계정이며 아이디는 osm, 해당 계정 도메인은 test.co.kr이다. 즉 test.co.kr내부에 있는 osm 계정 비밀번호는 12345
uid, gid는 내가 해당 서버에서 접속하려고 하는 계정의 정보이다.

```
appadmin:x:1003:1003::/app:/bin/bash
```

다음에는 삽질하지말자,,

