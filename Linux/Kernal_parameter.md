```
# TCP TIME_WAIT Setting
net.ipv4.tcp_tw_reuse = 1

# TCP Port Range Setting
net.ipv4.ip_local_port_range = 10240 65535
net.ipv4.tcp_max_tw_buckets = 1800000

# TCP Backlog Setting
net.core.netdev_max_backlog = 30000
net.core.somaxconn = 8192
net.ipv4.tcp_max_syn_backlog = 8192
```

🔹 TCP TIME_WAIT 관련
net.ipv4.tcp_tw_reuse = 1

의미: TIME_WAIT 상태의 소켓을 새로운 연결에서 재사용할 수 있게 허용.

용도: 짧은 시간에 많은 TCP 연결을 생성/종료할 때, TIME_WAIT 소켓이 너무 많이 쌓여서 포트 고갈이 생기는 걸 방지.

주의점: NAT 환경이나 클라이언트에서 서버로의 다중 연결 환경에서 잘못 쓰면 패킷 꼬임 발생 위험이 있음. (특히 클라이언트에서 켜는 건 비추천)

🔹 TCP Port Range 관련
net.ipv4.ip_local_port_range = 10240 65535

의미: 애플리케이션이 사용할 수 있는 동적 포트 범위 지정.

기본값은 보통 32768–60999 정도.

용도: 대규모 클라이언트 연결(예: Proxy, Load Balancer, DB Connection Pool)에서 더 많은 ephemeral port를 쓰기 위해 범위를 넓힘.

net.ipv4.tcp_max_tw_buckets = 1800000

의미: 시스템에서 동시에 유지할 수 있는 TIME_WAIT 소켓의 최대 개수.

용도: 초과하면 커널이 오래된 TIME_WAIT 소켓을 강제로 지움.
대규모 연결 환경에서 TIME_WAIT 소켓 때문에 메모리 잡아먹는 걸 방지.

🔹 TCP Backlog 관련
net.core.netdev_max_backlog = 30000

의미: 네트워크 인터페이스 카드(NIC)가 커널에 패킷을 전달할 때, 커널 큐에 쌓아둘 수 있는 수신 패킷 최대 큐 길이.

용도: 순간적으로 네트워크 트래픽이 몰려도 패킷 드롭이 안 나게 함.

net.core.somaxconn = 8192

의미: 애플리케이션에서 listen() 호출 시 backlog로 줄 수 있는 최대 대기 연결 수.

기본값은 보통 128.

용도: 서버에 동시 접속 요청이 폭주할 때, accept() 대기 큐가 커서 연결 거절이 덜 나도록.

net.ipv4.tcp_max_syn_backlog = 8192

의미: SYN 패킷을 받아서 아직 3-way handshake가 완료되지 않은 **반쯤 열린 연결(half-open)**의 최대 개수.

기본값은 256~1024 정도.

용도: 초당 수천~수만 개의 새로운 연결 요청이 몰리는 환경(예: 웹서버, API Gateway)에서 SYN Flood 같은 상황에 더 버티도록.
