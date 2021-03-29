# SSH 접속시 RSA 공유키 충돌 문제 해결


```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:*************************************.
Please contact your system administrator.
```

이유는 해당 IP 로 기존에 접속한 적이 있는 서버와 RSA 공유키를 교환한 상태에서,

기존 서버가 바뀌었기 때문이다. 이 경우 라즈베리파이에서 *******을 사용하다가 같은 LAN포트를 페도라를 설치한 노트북에 꼽았기에 같은 IP를 쓰게 된 상황이다.

위의 경고 메시지는 Man in the Middle Attack 이라는 일명 '중간자 공격'에 대해 경고한다. 즉, 기존에 서버가 알고있던 정보를 찾아서 따라갔더니- 기존과는 전혀 다른 서버로 접속되었다는 것이다.

하지만 이 경우는 운영자인 내가 고의적으로 변경한 것이기에, 해킹 등의 침해사고는 아니다. (정확히는 스푸핑)

이를 해결하기위해서는 다음과 같은 명령어를 통해 초기화를 시켜준다.

ssh-keygen -R [ IP or DomainName]


```
[root@shlc-prd-web01 /root/.ssh]$ ssh-keygen -R *******
# Host ******* found: line 1
/root/.ssh/known_hosts updated.
Original contents retained as /root/.ssh/known_hosts.old
```
