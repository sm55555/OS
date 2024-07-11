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

# Template to include the tag in the log file name
#template(name="DynFile" type="string" string="/var/log/%HOSTNAME%/%PROGRAMNAME%.log")

# Store Nginx access logs
if $programname == 'nginx-access' then ?DynFile
& ~

# Store Nginx error logs
if $programname == 'nginx-error' then ?DynFile
& ~

# Store other logs
*.* /var/log/other_logs.log
```

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
$InputFileFacility local6
$InputRunFileMonitor

# Nginx error log configuration
$InputFileName /var/log/nginx/error.log
$InputFileTag nginx-error:
$InputFileStateFile stat-nginx-error
$InputFileSeverity error
$InputFileFacility local7
$InputRunFileMonitor

# Forward Nginx access logs to IDC log server
local6.* @@<idc-log-server-ip>:514

# Forward Nginx error logs to IDC log server
local7.* @@<idc-log-server-ip>:514
```


