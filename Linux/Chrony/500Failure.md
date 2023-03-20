### chronyc -a makesep 시 500 Failure

1. chrony 최신버전으로 업데이트


2. 아래 옵션으로 변경
```
vi /etc/default/chrony

SYNC_IN_CONTAINER="yes"

```
