## [IDC nginx log to AWS EC2]

![image](https://github.com/sm55555/OS/assets/38831314/aa94f66b-be5b-4c78-b20d-caea019d04af)

#### [Security Group]

<img width="546" alt="image" src="https://github.com/sm55555/OS/assets/38831314/a51d5926-ceff-48c8-8da1-d97aa91db612">


#### [Server Config]

/etc/rsyslog.conf

```bash
# Load necessary modules
$ModLoad imudp
$UDPServerRun 514
$ModLoad imtcp
$InputTCPServerRun 514

module(load="imudp")
input(type="imudp" port="514")

local1.*            /var/log/nginx/error.log
local2.*            /var/log/nginx/access.log

```

The & ~ syntax in rsyslog configuration means "stop processing this message." It's a way to tell rsyslog that after handling this particular message with the specified rule, it should not continue to process it with any further rules.


#### [Client Config]

/etc/rsyslog.d/nginx-logs.conf

```bash
# Load the imfile module
$ModLoad imfile

# Nginx access log configuration
$InputFileName /var/log/nginx/access.log
$InputFileTag nginx-access:
$InputFileStateFile stat-nginx-access
$InputFileSeverity info
$InputFileFacility local1
$InputRunFileMonitor

# Nginx error log configuration
$InputFileName /var/log/nginx/error.log
$InputFileTag nginx-error:
$InputFileStateFile stat-nginx-error
$InputFileSeverity error
$InputFileFacility local2
$InputRunFileMonitor

# Forward Nginx access logs to IDC log server
local1.* @<idc-log-server-ip>:514

# Forward Nginx error logs to IDC log server
local2.* @<idc-log-server-ip>:514
```

대신 용량이 많으면 좀 발동이 늦게 걸린다.

[대용량 로그 최적화]

# /etc/rsyslog.conf - c6g.8xlarge 서버 및 다중 출력을 위한 v8.2 호환 고성능 설정

```
#################
# 전역 지시자 (GLOBAL DIRECTIVES)
#################

# 처리할 최대 메시지 크기를 64k로 넉넉하게 설정합니다.
global(maxMessageSize="64k")

# 디스크 보조 큐(Disk-Assisted Queue)가 사용할 작업 디렉토리를 지정합니다.
# 원격 전달 실패 시 로그를 임시 저장할 공간입니다.
global(workDirectory="/var/spool/rsyslog")


#################
# 모듈 (MODULES)
#################

# imudp: UDP 입력 모듈
# - threads: 32개의 vCPU 중 16개를 할당하여 네트워크로부터의 데이터 수집을 병렬화합니다.
# - batchSize: 한 번의 시스템 콜로 최대 256개의 메시지를 가져와 CPU 오버헤드를 줄입니다.
# - rcvbufSize: 커널 소켓 수신 버퍼 크기를 128MB로 요청하여 OS 수준의 패킷 손실을 방지합니다.
module(load="imudp"
       threads="16"
       batchSize="256"
       rcvbufSize="128m")

# impstats: 내부 성능 카운터 모니터링을 위한 모듈 (성능 검증에 필수)
module(load="impstats"
       interval="60"
       resetCounters="on"
       log.file="/var/log/rsyslog-stats.log"
       log.syslog="off")


#################
# 메인 큐 설정 (MAIN QUEUE CONFIGURATION)
#################

# 모든 입력은 이 메인 큐를 거칩니다. UDP 손실 방지를 위한 핵심 설정입니다.
main_queue(
    # queue.type: 예측 불가능한 트래픽 폭증에 유연하게 대응하기 위해 LinkedList 사용.
    queue.type="LinkedList"

    # queue.size: 64GiB의 넉넉한 메모리를 활용하여 인-메모리 큐를 5백만 개 메시지로 설정합니다.
    queue.size="5000000"

    # queue.workerThreads: 큐에서 메시지를 처리하는 작업 스레드를 16개로 설정하여 병목 현상을 방지합니다.
    queue.workerThreads="16"

    # queue.dequeueBatchSize: 한 번에 4096개의 메시지를 처리하여 큐 잠금 경합을 최소화하고 처리량을 극대화합니다.
    queue.dequeueBatchSize="4096"

    # queue.fullDelayMark: 큐가 98% (4,900,000개) 찼을 때 TCP와 같은 지연 가능한 입력을 차단합니다.
    #                      나머지 2%의 공간은 어떤 상황에서도 유실되면 안 되는 UDP 메시지를 위해 남겨둡니다.
    queue.fullDelayMark="4900000"
)


#################
# 입력 리스너 (INPUT LISTENERS)
#################

# 표준 UDP 포트 514에서 로그 수신
input(type="imudp" port="514")


#################
# 규칙 (RULES)
#################

# 규칙 1: local1 퍼실리티 로그를 access.log 파일에 기록
if $syslogfacility-text == 'local1' then {
    # action: 로컬 파일 쓰기는 매우 빠르므로 별도의 큐 없이 'direct' 모드로 직접 처리하여
    #         불필요한 오버헤드와 지연을 제거합니다.
    action(type="omfile"
           file="/var/log/nginx/access.log"
           queue.type="direct")
}

# 규칙 2: local3 퍼실리티 로그를 access2.log 파일에 기록
if $syslogfacility-text == 'local3' then {
    action(type="omfile"
           file="/var/log/nginx/access2.log"
           queue.type="direct")
}

# 규칙 3: 모든(*.*) 로그를 원격 서버로 전달
# 이 액션은 원격 서버 장애에 대비하여 반드시 자체적인 비동기 큐를 가져야 합니다.
action(
    type="omfwd"
    target="172.18.13.188"
    protocol="udp"

    # -- 원격 전달 전용 액션 큐 설정 --
    # queue.type: 비동기 처리를 위해 LinkedList 큐를 사용합니다.
    queue.type="LinkedList"

    # queue.filename: 큐 파일 이름을 지정하여 '디스크 보조(Disk-Assisted)' 모드를 활성화합니다.
    #                 원격 서버가 다운되면 로그가 이 파일에 기록되어 유실을 방지합니다.
    queue.filename="fwd_remote_server"

    # queue.size: 이 액션만을 위한 인-메모리 큐 크기를 10만개로 설정합니다.
    queue.size="100000"

    # queue.saveOnShutdown: rsyslog 종료 시 처리 못한 메시지를 디스크에 저장합니다.
    queue.saveOnShutdown="on"

    # action.resumeRetryCount: 원격 서버 접속 실패 시 무한 재시도(-1)합니다.
    action.resumeRetryCount="-1"
)
```

-------------
echo "net.core.rmem_max=67108864" | sudo tee -a /etc/sysctl.conf
echo "net.core.rmem_default=67108864" | sudo tee -a /etc/sysctl.conf
echo "net.core.netdev_max_backlog=30000" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p


