정상적인 파일이라도 아래와 같은 현상이 발생한다.

```
Failed to open/create the internal network 'HostInterfaceNetworking-VirtualBox Host-Only Ethernet Adapter #2' (VERR_INTNET_FLT_IF_NOT_FOUND).
Failed to attach the network LUN (VERR_INTNET_FLT_IF_NOT_FOUND).
Result Code: E_FAIL (0x80004005)
```

1. VirtualBox 를 Uninstall 합니다.

    - VM 이미지들은 그대로 유지되므로, 프로그램만 지워질뿐 VM은 삭제되지 않습니다.

2. 제어판 -> 네트워크 및 인터넷 -> 이더넷 -> 어댑터 옵션 변경 을 선택해서 VirtualBox 삭제후에도
    Virtual Host-Only Network interface 가 존재한다면 우클릭 -> 삭제 합니다.

<img width="526" alt="image" src="https://github.com/sm55555/OS/assets/38831314/654f0e6d-3c02-4d1c-b09b-1c25b5ffdd77">

3. Windows 재시작

4. 재시작 후, VirtualBox Installer를 관리자권한으로 실행하여 다시 Install 합니다.

5. VirtualBox Install 후에도 VM이 에러로 인해 실행이 되지 않습니다.

6. 다시 위의 제어판의 어댑터 옵션변경 창으로 들어갑니다.

7. VirtualBox를 다시 Install 했기 때문에 VirtualBox Host-Only Network interface가 다시 생성되어있습니다.

8. 만약 VirtualBox가 실행되어있다면 종료 후, VirtualBox Host-Only Network interface를 우클릭 -> 사용안함으로 변경합니다.

9. 다시 VirtualBox Host-Only Network interface를 우클릭 -> 사용함 으로 변경합니다.

10. 그후 VirtualBox 실행후 Host-Only network를 사용하는 VM이 정상구동됨을 확인하였습니다.


##### 출처 https://hand-over.tistory.com/18
