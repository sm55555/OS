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
