---
layout: default
comments: true
---

# VNC 를 이용한 Raspberry pi 화면 Mirroring 구현

## Linux VNC server
tightVNC, vnc4server, realVNC 등이 있지만 Ubuntu Gnome 의 vino 면 충분하다.

`$ vino-preferences`

## Raspberry Pi
여러개의 기기가 하나의 서버에 접속해 복사가 가능하다.

`$ vncviewer ipaddr`
