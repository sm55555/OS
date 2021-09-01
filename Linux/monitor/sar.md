# 리눅스 모니터링 설정

Sar 수집 관련 (기본적으로 분 단위는 설정이 되어서 인터넷 검색 필요)

sar 설정 관련 : vi /etc/cron.d/sysstat
sar 보기 : sar -f /var/log/sa/sa06 [해당 날짜 참고,,, 오늘은 6일이다.]

1초로 설정하는법

*/1 * * * * root /usr/lib64/sa/sa1 1 59

5초로 설정하는법

*/1 * * * * root /usr/lib64/sa/sa1 1 59 ; sleep 5 ; /usr/lib64/sa/sa1 1 1; sleep 5 ; 해당 문구 반복


### 메모리 부분 확인

sar -r -f /var/log/sa/sa06 -s HH:MM:SS -e HH:MM:SS

sar은 linux 특성상 유휴 공간을 캐시영역으로 사용하기 때문에 %memused가 훨씬높게 나옴
해당 부분은 폴스타 참고

### CPU 사용량 확인

sar -f /var/log/sa/sa06 -s HH:MM:SS -e HH:MM:SS
