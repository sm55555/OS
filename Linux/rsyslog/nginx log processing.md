## [IDC nginx log to AWS EC2]

![image](https://github.com/sm55555/OS/assets/38831314/aa94f66b-be5b-4c78-b20d-caea019d04af)


#### [Client Config]

```bash
# Load necessary modules
$ModLoad imudp
$UDPServerRun 514
$ModLoad imtcp
$InputTCPServerRun 514

# Template to include the tag in the log file name
template(name="DynFile" type="string" string="/var/log/%HOSTNAME%/%PROGRAMNAME%.log")

# Store Nginx access logs
if $programname == 'nginx-access' then ?DynFile

# Store Nginx error logs
if $programname == 'nginx-error' then ?DynFile

# Store other logs
*.* /var/log/other_logs.log
```
