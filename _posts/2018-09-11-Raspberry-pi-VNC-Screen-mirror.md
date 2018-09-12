---
layout: default
comments: true
---

# VNC 를 이용한 Raspberry pi 화면 Mirroring 구현

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

TODO: 구현중

## VNC client monitoring
VNC server 에서 연결된 client 의 상태를 감시한다. listen 사용

TODO: 구현중
