### 폴스타 설치 시 에러 상황

```
./NNPAgent/utils/INSTALL/AgentInstall: error while loading shared libraries: libstdc++.so.6: cannot open shared object file: No such file or directory
```

yum install libstdc++.so.6


```
./AgentInstall.sh: ./NNPAgent/utils/INSTALL/AgentInstall: /lib/ld-linux.so.2: bad ELF interpreter: No such file or directory
```

yum install ld-linux.so.2

