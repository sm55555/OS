### sudo 권한 할당

```
vi /etc/sudoers
```

appadmin 아래와 같이 추가

```
## Next comes the main part: which users can run what software on
## which machines (the sudoers file can be shared between multiple
## systems).
## Syntax:
##
##      user    MACHINE=COMMANDS
##
## The COMMANDS section may have other options added to it.
##
## Allow root to run any commands anywhere
root    ALL=(ALL)       ALL
appadmin        ALL=(ALL)       ALL

```

되지 않으면 가장밑에 추가해주자

```
#includedir /etc/sudoers.d
appadmin        ALL=(ALL)       NOPASSWD: AL
```
