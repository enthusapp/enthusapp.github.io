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
