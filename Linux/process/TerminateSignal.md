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
