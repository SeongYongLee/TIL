## Cross Browsing

웹 표준에 따라 개발을 하여 서로 다른 OS 또는 플랫폼에 대응하는 것을 말한다.

브라우저의 렌더링 엔진이 다른 경우에 인터넷이 이상없이 구현되도록 하는 기술이다.

웹 사이트를 서로 비슷하게 만들어 어떤 환경 에서도 이상없이 작동되게 하는데 그 목적이 있다.

즉, 어느 한쪽에 최적화되어 치우치지 않도록 공통요소를 사용하여 웹 페이지를 제작하는 방법을 말한다.

### 크로스 브라우징은 동일성을 의미하지 않는다. 동등성(등가성)을 의미한다.

크로스 브라우징을 이야기 할 때 종종 볼 수 있는 글이 '모든 브라우저에서 똑같이 보이게'라고 하는 것인데 당장 네이버에서 크로스 브라우징을 검색해만 보아도 이러한 글을 쉽게 접할 수 있다. 고용노동부에서 제공하는 한국직업사전 조차 크로스 브라우징에 대해 '어떤 웹 브라우저를 써도 화면이 똑같이 나오고'라고 기재되어 있다. 이는 잘못 된 내용이라고 한다.

한국소프트웨어진흥원 공개SW지원센터에서 발간한 것으로 보이는 'CSS Browsing 가이드'라는 문서가 있다. 여기서는 크로스 브라우징에 대해 다음과 같이 설명한다.

`Cross Browsing이란 적어도 표준 웹기술을 채용하여 다른 기종 혹은 플랫폼에 따라 달리 구현되는 기술을 비슷하게 만듦과 동시에 어느 한쪽에 최적화되어 치우지지 않도록 공통 요소를 사용하여 웹 페이지를 제작하는 기법을 말하는 것이다. 또한, 지원할 수 없는 다른 웹 브라우저를 위한 장치를 구현하여 모든 웹 브라우저 사용자가 방문했을 때 정보로서의 소외감을 느끼지 않도록 하는 방법론적 가이드를 의미하는 것이다.`

### 대응 방법

#### 브라우저 파악

개발 기획 시 우리가 개발 할 기능들을 정의하고, 그 기능들을 지원할 브라우저를 우선 파악한다.

핵심적인 기능은 모든 브라우저에서 동작해야 하지만, 부가적인 기능은 구 브라우저에서도 소외감이 느끼지 않게 해야한다. 동작이 되지 않으면 안되며 정적으로라도 렌더링은 되어야한다.

이것저것 신경쓰다가 정작 중요한 비즈니스 로직 등을 놓치는 우를 범할 수 있으니 조심해야한다.

#### 라이브러리 파악

호환성 이슈를 해결하기 위한 아주 좋은 전략이지만 라이브러리가 비대해질 수 있고 잘 관리해야하는 cost가 발생한다.

#### 기능 탐지

직접 구현시 각 브라우저가 해당 기능을 지원하는지 Feature detection 해본다.

- [Feature detection, Feature inference, UA String](https://github.com/SeongYongLee/TIL/tree/main/FrontEnd/Feature-Detection-Feature-Inference-UA-String)

#### 툴 사용

- Cross-Browser Compatibility

    각 브라우저 들이 웹표준을 지키고 있는지 여러가지 툴들을 사용하여 확인한다.

- reset, css

    CSS의 경우 browser 기본 스타일이 제각각인 경우가 있다. 동일한 스타일을 적용하기 위해 defalut 값을 초기화 시킬 필요가 있다. 라이브러리를 사용하는 경우 무작정 C&P 하지 말고, 어떤 의미에서 초기화 시키는지 알고 사용해야 한다.
    
    - [Normalize vs Reset](https://github.com/SeongYongLee/TIL/tree/main/FrontEnd/Normalize-vs-Reset)

- css prefix

    모든 브라우저에서 지원하는 호환 프로퍼티를 먼저 정의하고 css3에서 지원하는 프로퍼티를 나중에 정의해서 사용한다.

    ```css
    #menu {
        -webkit-border-radius: 15px;
        -moz-border-radius: 15px;
        border-radius: 15px;
    }
    ```

### Reference

- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/FrontEnd

- https://asfirstalways.tistory.com/237

- https://mulder21c.github.io/2019/01/30/what-is-cross-browsing

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/FrontEnd)