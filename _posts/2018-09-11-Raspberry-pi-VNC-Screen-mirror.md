---
layout: default
comments: true
---

# VNC 를 이용한 Raspberry pi 화면 Mirroring 구현

## 문제점
Client 의 영상 응답속도 문제가 있다. Server 의 화면과 동영상의 해상도를 낮추면 응답속도 문제가 적게 나타난다.(응답속도 문제를 확인하려면 영상을 전체화면으로 재생하고 변화율이 큰 동영상을 재생하면 된다.) 고용량 네트워크 환경에서 어떻게 변하는지, vino 설정 변경이 가능한지는 이후 확인해야할 숙제이다.

## Linux VNC server
tightVNC, vnc4server, realVNC 등이 있지만 Ubuntu Gnome 의 vino 면 충분하다.

`$ vino-preferences`

## Raspberry Pi
여러개의 Raspberry Pi 가 하나의 서버에 접속해 화면 복사가 가능하다. `man vncviewer` 의 내용을 참조하여 네트워크과 적용 환경에 맞게 옵션을 선택하면 된다.

`$ vncviewer ipaddr`

 tightVNC 를 사용할때는 `-compresslevel` 을 0으로 설정해야 화면 떨림이 사라진다. Raspberry Pi의 CPU 성능으로는 compress 기능을 제대로 활용할 수 없는것으로 보인다. compress 기능을 사용하지 못하면 네트워크 부하가 증가하는 단점이 있다.
 
 tightVNC 가 아닌 raspberry pi 에 설치되어 있는 기본 vncviewer 에는 compress 옵션이 없다. 그대로 사용 가능하다.

## VNC server monitoring
네트워크 상황이 좋지 않을 경우 VNC 연결이 끊기게 된다. VNC 서버와의 연결을 지속적으로 확인하고 연결이 끊기면 vncviewer 를 재실행 시킨다.

구현: [https://github.com/enthusapp/vncmonitor](https://github.com/enthusapp/vncmonitor)

단점, vncviewer 의 로그가 충분하지 않아 동작이 잘 안되고 있는지 육안이 아니고서는 확인이 어렵다. netcat 으로 vncserver port 를 확인하는 방식을 사용했지만 정공법은 아닌것 같다. open source vnc client 들이 많지만 코드 복잡도가 높아 투자시간이 많이 필요해 보인다.

##### open source vnc client 평가
- noVNC
  - vnc server 의 데이터를 websocket 으로 변환하여 html5 기반 화면에 투사
  - JS 기반으로 가장 가볍고 webview 기반 어플에서는 사용이 쉽다.
  - 기본적으로 compressed 데이터로 전달되기 때문에 느리거나 true color 전달이 안된다.
- remmina
  - GTK+ 기반 vnc client
  - 기본적으로 compressed 를 쓰도록 되어 있는데, 코드를 수정하면 안쓸수도 있을것 같다.
  - 안정성이 좋아보이고 가장 open source 분석을 시작할만 코드 일수 있다.
- tigerVNC
  - real VNC client 에 가장 가까운 open source vnc
  - 안정성이 궁금하다.

## VNC client monitoring
VNC server 에서 연결된 client 의 상태를 감시한다. listen 사용

TODO: 구현중
