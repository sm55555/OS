# ldd

```
※ 요약
리눅스 명령어 ldd는 지정한 프로그램의 라이브러리 의존성을 확인할 때 사용하는 명령어다.

※ 경로
/usr/bin/ldd

※ 사용법
ldd [옵션] 파일명
```

## 예제

```
$ ldd `which openssl`

        linux-vdso.so.1 (0x00007ffdef5e6000)
        libssl.so.1.1 => /usr/lib/x86_64-linux-gnu/libssl.so.1.1 (0x00007fc7e741c000)
        libcrypto.so.1.1 => /usr/lib/x86_64-linux-gnu/libcrypto.so.1.1 (0x00007fc7e6f51000)
        libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007fc7e6d32000)
        libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007fc7e6941000)
        libdl.so.2 => /lib/x86_64-linux-gnu/libdl.so.2 (0x00007fc7e673d000)
        /lib64/ld-linux-x86-64.so.2 (0x00007fc7e795c000)
```

만약 필요한게 없을 시 Not Found라고 뜬다..
