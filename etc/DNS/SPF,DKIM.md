### SPF,DKIM 이란 ?

```
SPF(Sender Policy Framework)
DKIM(DomainKeys Identified Mail)

이메일 발신자가 정말 자기 자신이 맞는지, 위조되지 않았는지 검증하기 위해서 사용 된다.
SPF, DKIM 설정이 없으면 메일보낼 때 이메일을 차단하거나, 스팸으로 분류 될 수 있다.
예를들어 이메일 마케팅 서비스 업체를 사용하면 발신자 이메일 주소, 실제 발송하는 서버 도메인 다를 수 있다.
"user@domain.com" 발신자 이메일로 발송할 때, 실제 발송되는 서버는 "send.com"이 된다. 이런 경우 "send.com"에 대한 레코드를 "domain.com"에 등록하여
발신자가 위조 되지 않았다는 것을 네이버, 다음 구글 같은 이메일 수신 서버에게 알려줘야 하기에 SPF, DKIM 설정이 필요하다.
```






