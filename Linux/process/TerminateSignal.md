## How to run script linux shutdown


```
vi /usr/lib/systemd/system/shutdown.service
```

```
[Unit]
Description=Run Script at shutdown
Before=shutdown.target
Requires=network-online.target network.target
Wants=network-online.target
After=network-online.target

[Service]
KillMode=none
ExecStart=/bin/true
ExecStopPost=/home/test.sh
RemainAfterExit=true
Type=oneshot

[Install]
WantedBy=multi-user.target
```

```
/home/test.sh
```

```
systemctl stop test.service
```

```
chmod 755 /home/test.sh
systemctl daemon-reload
systemctl enable shutdown.service
```

이렇게 구성하면 서버가 켜져있고 shutdown.service가 프로세스 내려간 상태라도 서버 shutdown 시 /home/test.sh 가 동작한다.
