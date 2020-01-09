# Command

## Linux

enviroment : amazon linux2 (centOS)


### netstat

~~~
[ec2-user@ip-10-0-0-86 ~]$ netstat -anp
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      -                   
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      -                   
tcp        0    416 10.0.0.86:22            211.206.114.80:41251    ESTABLISHED -                   
tcp6       0      0 :::111                  :::*                    LISTEN      -                   
tcp6       0      0 :::22                   :::*                    LISTEN      -                   
udp        0      0 0.0.0.0:753             0.0.0.0:*                           -                   
udp        0      0 127.0.0.1:323           0.0.0.0:*                           -                   
udp        0      0 0.0.0.0:68              0.0.0.0:*                           -                   
udp        0      0 0.0.0.0:111             0.0.0.0:*                           -   
...
~~~

netstat shows the communication status of the network interface installed on the host

### find 

~~~
sudo find / -name "*aaaaa*"
~~~
It prints the files that contain the corresponding input

You have to wirte "sudo" because linux find command is search from root directory


* * *


## Window

~~~

~~~
