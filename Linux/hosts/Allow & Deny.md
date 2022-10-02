# hosts.deny hosts.allow

Priority  host.allow >> hosts.deny

Linux provides two files host.allow and host.deny to allow and deny access to SSH port.
you simply need to add your trusted IP addresses to host.allow file, and add suspicious IP address in host.deny file

### Allow SSH Access

Open terminal and run the following command to open host.allow file.

```
$ vi /etc/host.allow
```

If you want to allow access from multiple IP addresses, add them in a comma-separated manner

```
sshd: 54.43.32.11, 11.22.33.44
```

If you want to allow access from range of IP addresses use the CIDR notation to allow an IP address range.

```
sshd: 54.43.32.0/24, 11.22.33.0/24
```

Finally, open terminal and run the following command

```
systemctl restart sshd
```

### Restrict SSH Access

Similarly, open terminal and run following command to open host.deny file.

```
$ vi /etc/host.deny
```

Add the following line to deny access from ip 44.33.22.11

```
sshd: 44.33.22.11
```

If you want to restrict access from range of IP addresses use the CIDR notation to allow an IP address range.

```
sshd: 44.43.32.0/24, 34.43.32.0/24
```

Finally open terminal and run the following command

```
systemctl restart sshd
```
