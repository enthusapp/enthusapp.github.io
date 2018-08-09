# Raspberry PI 에서 Flash 파일 재생
## Raspberry PI 에서 Flash Player library 찾기
chrome 에서 주소창에 `chrome://plugins` 입력하고 세부정보 버튼을 클릭하면, Electron.JS 가 flash 파일 재생할때 필요한 `libpepflashplayer.so` 라이브러리의 위치를 확인할 수 있다.

![chrome plugins 확인](/assets/img/libpepflashplayer.jpg)

`libpepflashplayer.so` 파일을 Electron.JS 프로젝트의 루트폴더에 복사한다.

## index.html 작성
index.html 에 embed 로 Flash 파일 추가하고 main.js 에서 index.html 을 load 하면 재생시작
