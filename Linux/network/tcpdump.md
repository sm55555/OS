### 자주 쓰이는 명령어

```
tcpdump -i eth0: 인터페이스 eth0을 보여줌
tcpdump -i eth0 -c 10: 10개만 덤프
tcpdump -i eth0 tcp port 80: TCP 80 포트로 통신하는 패킷 덤프
tcpdump -i eth0 src 192.168.0.1: 출발지 IP가 192.168.0.1인 패킷 덤프
tcpdump -i eth0 dst 192.168.0.1: 목적지 IP가 192.168.0.1인 패킷 덤프
tcpdump -i eth0 src 192.168.0.1 and tcp port 80: 목적지 IP가 192.168.0.1이면서 TCP 80 포트인 패킷 보여줌
tcpdump -i eth0 dst 192.168.0.1: 목적지IP가 192.168.0.1인 패킷 보여줌
tcpdump host 192.168.0.1: 특정 호스트 IP로 들어오거가 나가는 양방향 패킷 모두 덤프
tcpdump src 192.168.0.1: 특정 호스트 중에서 출발지가 192.168.0.1인 것만 덤프
tcpdump dst 192.168.0.1: 특정 호스트 중에서 목적지가 192.168.0.1인 것만 덤프
tcpdump port 3389: 포트 양뱡항으로 3389이면 덤프
tcpdump src port 3389: 출발지 포트가 3389인 것만 덤프
tcpdump dst port 3389: 목적지 포트가 3389인 것만 덤프
tcpdump udp and src port 53: UDP이고 출발지 포트가 53이면 덤프
tcpdump src 192.168.0.1 and not dst port 22: 출발지 IP가 192.168.0.1이고 목적지 포트가 22 가 아닌 패킷 덤프
tcpdump -w tcpdump.log: 결과를 파일로 저장(텍스트가 아닌 바이너리 형식으로 저장)
tcpdump -r tcpdump.log: 저장한 파일을 읽음
```

FTP 관련 dump

```
tcpdump -i eth0 host 172.0.0.1 and not host 10.20.103.73 and port 22
```
