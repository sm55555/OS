### 포트 관련 이벤트 뷰어

만약 포트를 다 사용한다면 서버는 정상이지만 서버에서 아웃바운드로 새로운 요청이 안될 수 있다.

![image](https://user-images.githubusercontent.com/38831314/135713675-017fe782-e16d-4e2f-9fdb-efca3954ec96.png)


작업 관리자에서 핸들 개수 확인

![image](https://user-images.githubusercontent.com/38831314/135713704-92297c49-0521-4611-a24e-f622b6f10f73.png)

Get-NetTcpConnection 으로 점검
