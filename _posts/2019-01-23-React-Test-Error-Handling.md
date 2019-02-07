---
layout: default
comments: true
---

# API 에러
**API 바꾸기**

React 의 unit test 를 위해서는 DOM simulator 인 enzyme 를 사용한다.
하지만 web-animate-api 와 같은 최신 api 를 사용하면 JSDOM 에서 지원하지 않아 에러가 발생하게 된다.
그럴때 전체 setupTest.js 에서 전체 HTML element 에 fake api 를 추가하면 에러 없이 테스트가 가능하다.

우선 [https://airbnb.io/enzyme/docs/guides/jsdom.html](https://airbnb.io/enzyme/docs/guides/jsdom.html) 의 내용을 추가하고 아래의 코드도 추가,

```
global.window.HTMLElement.prototype.animate = () => { };
```

기능을 확장한다면 해당 api 를 이용한 테스트도 가능할 것 같다.

마찬가지로 [https://github.com/jsdom/jsdom/issues/1721](https://github.com/jsdom/jsdom/issues/1721) 에도 비슷한 내용이 설명되어 있다.
JSDOM 에서 지원하지 않는 API 는 테스트 과정에서 에러가 발생하게 된다.
마지막 답변처럼 `() => {}` 와 같은 no operation function 을 추가하는 것이 일반적인 방법으로 보인다.

**Instance 바꾸기**

API 문제가 발생하는 곳을 별도의 함수로 분리하고, 그 함수를 테스트 직전 교체한다.

```
component.instance().download = () => { };
```

에러를 막을 뿐만 아니라, 문제 발생전에 입력되는 parameter 의 테스트도 가능하다.
문제의 API 동작 테스트는 수동 테스트로 하거나, Web API 의 기본 동작이라 테스트 필요가 없을 수 있기 때문에 최종 출력값 확인을 위한 방법으로 사용이 가능하다.
