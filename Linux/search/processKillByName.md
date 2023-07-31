nginx 관련된 프로세스  kill 방법

```
ps -ef | grep nginx | awk '{print $2}' | xargs kill -9
```
