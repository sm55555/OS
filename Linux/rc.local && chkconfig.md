### rc.local 파일 참고


ex ) appadmin 전환 후 아파치(서비스 소유권 자 appadmin) 재기동
```cmd
vi /etc/rc.d/rc.local

su - appadmin -c /data/was/httpd/sbin/start.sh

```

### rc.local 검증방법

```
systemctl status rc-local.service
```
정상적으로 떠야함 그렇지 않으면 아래와 같이 뜬다.

![image](https://user-images.githubusercontent.com/38831314/137698029-3202e855-33bc-43c9-9158-433d6e862768.png)

jboss 관련 에러는

Oct 18 17:24:44 HGDEV-WAS2 rc.local[6578]: /data/was/domains/hgdev-was2/bin/start.sh: line 4: ./env.sh: No such file and Directory

./env.sh 주소가 상대 주소 잘못 작성되어 참조 실패 원인 -> 절대 주소로 변경


오류 내용
```
-- The start-up result is done.
Oct 18 17:24:44 HGDEV-WAS2 su[6627]: pam_unix(su-l:session): session opened for user jboss by (uid=0)
Oct 18 17:24:44 HGDEV-WAS2 rc.local[6578]: /data/was/domains/hgdev-was2/bin/start.sh: line 4: ./env.sh: No such file and Directory
Oct 18 17:24:44 HGDEV-WAS2 su[6627]: pam_unix(su-l:session): session closed for user jboss
Oct 18 17:24:44 HGDEV-WAS2 systemd[1]: rc-local.service: control process exited, code=exited status=1
Oct 18 17:24:44 HGDEV-WAS2 systemd[1]: Failed to start /etc/rc.d/rc.local Compatibility.
-- Subject: Unit rc-local.service has failed
```


### chkconfig 참고

리스트 조회
```
chkconfig --list
```

httpd 같은 서비스는 이렇게 설정 가능하다
```
chkconfig httpd on
```
