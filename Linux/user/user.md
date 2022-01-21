# 사용자 관리

#### 사용자 비밀번호 목록

#### 접속 방법 /etc/shadow


만약 비밀번호를 잃어버렸다면 2번째 탭 내용을 전부다 공백으로 바꾸어버리고 passwd [사용자]로 비밀번호 셋팅...


#### 사용자 삭제 시

-r 을 붙여주면 홈디렉토리 까지 삭제

```

userdel -r [username]


```

#### /etc/skel

신규 사용자 생성시 /etc/ske 파일을 복사하여 만들어진다.


#### 옵션 없이 사용자를 생성했을 때 설정

```

[root@test_d skel]# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes

```

### 홈 디렉토리 변경

testuser의 홈디렉토리를 /var/test/로 변경 요청

```cmd
usermod -d 폴더위치 아이디
```

```cmd
usermod -d /var/test/ testuser
```


