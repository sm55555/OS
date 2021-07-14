## Pagefile.sys 이란

Pagefile.sys란 리눅스의 swap 메모리 처럼 메모리가 부족 시 하드디스크의 일부분을 메모리 용도로 사용하는 것입니다.


## C 드라이브 용량 부족 시 Pagefile.sys 이전

[Tip] Pagefil.sys를 C드라이브 말고 다른곳에 옮겨도 블루스크린등 에러가 떳을 떄 덤프 생성이 가능하다.

1. 내 컴퓨터 -> 고급 시스템 설정

<img src="https://user-images.githubusercontent.com/38831314/125555306-7b36c4d0-3234-472b-a233-1ec27db66be7.png" width="50%" height="50%"/>

2. 고급 -> 설정

<img src="https://user-images.githubusercontent.com/38831314/125555349-dbf68f88-0cca-48ed-bb8f-5243ae4dc080.png" width="50%" height="50%"/>

3. 변경

<img src="https://user-images.githubusercontent.com/38831314/125555399-7aaa48d7-9df6-4d7d-a4c1-6bc278f3217b.png" width="50%" height="50%"/>

4. 기존의 C 드라이브 페이징 파일 없음 설정 클릭 -> 상단에 페이징 파일 크기(MB)에서 없는걸 확인

<img src="https://user-images.githubusercontent.com/38831314/125555430-d78f3430-f2de-4f58-b2f2-9f8c6cc736a5.png" width="50%" height="50%"/>

5. 옮기려는 드라이브에 -> 시스템이 관리하는 크기 클릭 -> 페이징 파일 크기(MB) [시스템에서 관리] 확인 

<img src="https://user-images.githubusercontent.com/38831314/125555537-f6421140-980a-428e-bac0-5f22ed3ab984.png" width="50%" height="50%"/>
