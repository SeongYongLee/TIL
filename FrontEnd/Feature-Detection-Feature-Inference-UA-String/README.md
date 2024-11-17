## Feature detection, Feature inference, UA String

사용자의 브라우저나 환경에 특정 웹 기술 기능이 있는지 확인하는 방법이다.

### Feature Detection (기능 감지)

Feature Detection은 브라우저가 특정 코드 블록을 지원하는지에 따라 다른 코드를 실행하도록 하는 방법이다.

```js
if ("geolocation" in navigator) {
  // navigator.geolocation를 사용할 수 있습니다
} else {
  // 부족한 기능 핸들링
}
```

[Modernizr](https://modernizr.com/)는 Feature detection을 처리 할 수 있는 훌륭한 라이브러리다.

Modernizr는 사용자의 브라우저에서 차세대 웹 기술의 가용성을 자동으로 감지하는 작은 JavaScript 코드이다. "UA 스니핑"을 기반으로 브라우저의 전체 범위를 블랙리스트에 올리는 대신 Feature Detection을 사용 하여 브라우저 의 실제 기능을 기반으로 사용자의 경험을 쉽게 조정할 수 있다.

### Feature Inference (기능 추론)

Feature inference는 Feature detection과 마찬가지로 기능을 확인하지만 해당 기능이 존재한다고 가정한 후 사용하는 방법이다.

```js
if (document.getElementsByTagName) {
  element = document.getElementById(id);
}
```

Feature detection이 더 확실한 방법이기에 이 방법은 권장하지 않는다.

### UA String (UA 문자열)

네트워크 프로토콜 피어가 요청하는 소프트웨어 유저 에이전트의 응용 프로그램 유형, 운영 체제, 소프트웨어 공급 업체 또는 소프트웨어 버전을 식별할 수 있도록 해주는 browser-reported String이다.

`navigator.userAgent` 를 통해 접근 할 수 있다. 하지만 문자열은 구문 분석하기 까다로우며 스푸핑될 수 있다. 예를 들어, Chrome은 Chrome과 Safari 모두 보고된다. Safari를 감지하기 위해서는 Safari 문자열이 있는지와 Chrome 문자열이 없는지 확인해야 한다.

이 방법은 오래된 관행이며 권장하지 않는다.

### Reference

- https://github.com/yangshun/front-end-interview-handbook/blob/master/contents/kr/javascript-questions.md

- https://rlynjb.medium.com/js-interview-question-what-s-the-difference-between-feature-detection-feature-inference-and-76d2e4956a9b

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/FrontEnd)
