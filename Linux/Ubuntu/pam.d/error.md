### passwd가 아래 처럼 안되는 경우

```
passwd: Authentication token manipulation error
passwd: password unchanged
```

pam-auth-update 명령어 실행 후 전부 다 체크한 다음 적용하면 된다.

되지 않는다면 /usr/lib/x86_64-linux-gnu 파일 개수, tail -10f /var/log/auth.log 확인 ! 

