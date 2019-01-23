---
layout: default
comments: true
---

### 최신 API 에러
React 의 unit test 를 위해서는 DOM simulator 인 enzyme 를 사용한다.
하지만 web-animate-api 와 같은 최신 api 를 사용하면 JSDOM 에서 지원하지 않아 에러가 발생하게 된다.
그럴때 전체 setupTest.js 에서 전체 HTML element 에 fake api 를 추가하면 에러 없이 테스트가 가능하다.

우선 [https://airbnb.io/enzyme/docs/guides/jsdom.html](https://airbnb.io/enzyme/docs/guides/jsdom.html) 의 내용을 추가하고 아래의 코드도 추가,

```
global.window.HTMLElement.prototype.animate = () => { };
```

기능을 확장한다면 해당 api 를 이용한 테스트도 가능할 것 같다.
