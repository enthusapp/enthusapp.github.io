---
layout: default
comments: true
---

# FFMPEG for Raspberry Pi

## FFMPEG wiki 에 나와있는 Raspberry Pi 용 compile 방법
* [https://trac.ffmpeg.org/wiki/CompilationGuide/RaspberryPi](https://trac.ffmpeg.org/wiki/CompilationGuide/RaspberryPi)

작성된지 오래되서 그런지 쉽게 안된다. 이런저런 방법으로 고쳐서 성공했지만 실행하면서 에러가 발생한다. cross-compile 환경 설정 문제로 보인다.

## FFMPEG wiki 에 나와있는 Ubuntu 용 compile 방법
* [https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu](https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu)

cross-compile 문제를 해결하기 위해 Raspberry Pi 에서 직접 compile 을 돌려봤다. 최신 Ubuntu 와 속도에서 차이도 별로 안나고 쉽게 컴파일이 완료되었다.

apt-get 으로 설치가 안되는 필수 library, cmake 는 직접 다운받아서 make/make install 로 해결하였다.

#### 사용한 compile 명령어
```
PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure \
  --prefix="$HOME/ffmpeg_build" \
  --pkg-config-flags="--static" \
  --extra-cflags="-I$HOME/ffmpeg_build/include" \
  --extra-ldflags="-L$HOME/ffmpeg_build/lib" \
  --extra-libs="-lpthread -lm" \
  --bindir="$HOME/bin" \
  --enable-gpl \
  --enable-libass \
  --enable-libfreetype \
  --enable-libmp3lame \
  --enable-libopus \
  --enable-libvorbis \
  --enable-libx264 \
  --enable-nonfree && \
PATH="$HOME/bin:$PATH" make && \
make install && \
hash -r
```

__결론: Ubuntu 용 compile 방법을 참조해서 Raspberry Pi 에서 compile 하면됨__
