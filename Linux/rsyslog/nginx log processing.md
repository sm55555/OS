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

