---
layout: default
comments: true
---

# Raspberry Pi 소소한 팁들

## Screenshot
Scrot 설치/실행한다. 자세한 링크: [https://www.imore.com/how-take-screenshot-raspberry-pi](https://www.imore.com/how-take-screenshot-raspberry-pi)

## Node.JS 최신버젼으로 설치
[https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04)

## Systemd 으로 프로그램 실행하기
[http://www.diegoacuna.me/how-to-run-a-script-as-a-service-in-raspberry-pi-raspbian-jessie/](http://www.diegoacuna.me/how-to-run-a-script-as-a-service-in-raspberry-pi-raspbian-jessie/) 참조, 만약 GUI 를 실행하려면 `[Unit]` 에 `User=root` 를 추가하고 `[Service]` 에는 `Environment=DISPLAY=:0.0` 과 사용자 인증을 위한 `Environment=XAUTHORITY=/home/dogs/.Xauthority` 변수를 추가해야 한다.

##### Ubuntu 에서 GUI 프로그램 systemd 로 실행하기
User=root -> User=(gui user name) 변경하여 [Service] 로 위치를 옮겨야 한다.

##### Systemd 로그 출력
systemd 를 사용하면 무엇보다 로그를 /var/log 아래서 관리할수 있다는 점이 편리하다. 로그 rotation 나 시간단위 backup 및 로그 삭제를 rlogsys 에서 알아서 해주니 로그 오버플로우, 로그 백업에 대한 걱정을 안해도 된다. python 프로그램의 경우 `-u` 옵션을 실행라인에 추가해야 buffering 없이 syslog 에 출력된다.

정보출처:[https://unix.stackexchange.com/questions/395479/how-to-keep-python-script-running-as-a-systemd-service](https://unix.stackexchange.com/questions/395479/how-to-keep-python-script-running-as-a-systemd-service)

## Raspberry Pi sdcard 작은 size 로 image 백업 
1. [dd 와 gzip 을 사용한 방법](http://www.seleads.com/dd-used-space-only-image-file-using-gzip-solved/) -> 보관하는 이미지의 크기는 줄어들지만 읽고 쓰는 시간이 길어져 win32 imager 대신 쓸수는 없다. 하지만 작은 사이즈의 sdcard 를 사용해야 할때는 필요할 수 있다. 같은 회사 제품도 실제 sector 크기가 다르기 때문에 실제 구매를 해봐야만 sdcard 의 sector 수를 알수 있는 것으로 보인다. 한편, dd 는 기본적으로 더 작은 사이즈로 image 를 만들지 못한다. 파일 시스템이 데이터를 파티션 섹터에 분산하여 저장하기 때문인것으로 보인다.
1. [rsync 사용](https://www.ostechnix.com/backup-entire-linux-system-using-rsync/) -> 부팅안됨, 파일복사 방법 기반 재확인이 필요하다.
1. resize2fs ?
1. 정답: dd 와 rsync 사용한 [rpi-clone](https://github.com/billw2/rpi-clone)

## Raspberry Pi 부팅과정에서 VNC client 
[https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=71698](https://www.raspberrypi.org/forums/viewtopic.php?f=28&t=71698)

## NTFS sd card mounting error
`NTFS-fs error (device sdb1): load_system_files(): $LogFile is not clean.  Mounting read-only.  Mount in Windows.`와 같은 문제가  `apt-get install ntfs-3g` 으로 해결

## Sdcard 사이즈 변경
[https://raspberrypi.stackexchange.com/questions/499/how-can-i-resize-my-root-partition](https://raspberrypi.stackexchange.com/questions/499/how-can-i-resize-my-root-partition)

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
미확인, 실외의 열악한 환경(열 및 불안정 전원)에 의한 sdcard 파손으로 추정됨

#### 해결방법
<code>fsck</code> 를 이용한 수정 방법이 많이 검색되지만, 그래도 복구가 안되는 경우가 있는 것 같음. 일단 sdcard 를 변경. 근본적인 해결책과 원인 분석은 아직 

[https://github.com/cyoung/stratux/issues/688](https://github.com/cyoung/stratux/issues/688)
