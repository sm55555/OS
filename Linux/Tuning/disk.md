# 디스크 I/O 병목줄이기

모든 파일 시스템은 3가지 timestamp 기능으로 파일의 변경 사항을 관리한다. 그 중에 atime은 제일 빈번하게 발생하면서 성능에 영향을 많이 끼친다.

```
파일시스템은 3가지의 시간을 관리한다.
1) ctime : 마지막 생성 / 수정된 시간
2) mtime : 마지막 변경된 시간
3) atime : 마지막 읽은 시간
```

noatime,nodiratime를 fstab에 추가해준다.
 
```
# vi /etc/fstab
/dev/sdc1     /mount-point     ext4      defaults,noatime,nodiratime     1 2
```
