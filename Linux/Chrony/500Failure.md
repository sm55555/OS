### chronyc -a makestep 시 500 Failure

1. chrony 최신버전으로 업데이트


2. 아래 옵션으로 변경
```
vi /etc/default/chrony
SYNC_IN_CONTAINER="yes"

```

2번으로 하면 chronyc -a makestep는 되지만 timedatectl set-ntp true는 안된다. 되게 하려면 1번으로 설정
