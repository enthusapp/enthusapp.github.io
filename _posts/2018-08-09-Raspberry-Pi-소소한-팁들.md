---
layout: default
comments: true
---

# Raspberry Pi 소소한 팁들

## Screenshot
Scrot 설치/실행한다. 자세한 링크: [https://www.imore.com/how-take-screenshot-raspberry-pi](https://www.imore.com/how-take-screenshot-raspberry-pi)

## Node.JS 최신버젼으로 설치
[https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04)

## File System 죽는 문제
<code>cat /var/log/boot.log</code> 명령어로 File System 문제가 발생하는지 확인
```
cat /var/log/boot.log

[    4.367629] systemd-fsck[215]: fsck.fat 3.0.27 (2014-11-12)
[    4.369367] systemd-fsck[215]: 0x41: Dirty bit is set. Fs was not properly unmounted and some data may be corrupt.
[    4.371040] systemd-fsck[215]: Automatically removing dirty bit.
[    4.372591] systemd-fsck[215]: Performing changes.

```

#### 원인
미확인, 실외의 열악한 환경(열 및 불안정 전원)에 의한 파손으로 추정됨

#### 해결방법
<code>fsck</code> 를 이용한 수정 방법이 많이 검색되지만, 그래도 복구가 안되는 경우가 있는 것 같음. 일단 sdcard 를 변경. 근본적인 해결책과 원인 분석은 아직 

[https://github.com/cyoung/stratux/issues/688](https://github.com/cyoung/stratux/issues/688)
