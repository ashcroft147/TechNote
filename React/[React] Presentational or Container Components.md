## Presentational Components
 - 화면에 보여지는 것에 관심을 갖는다
    - DOM markup or style 의 것들을 포함
 - this.props.children 을 담는다.
 - Redux or Store와 연관되지 않는다.
 - 데이터의 로딩 같은 것에 관심을 두지 않는다. 
    - 데이터나 Callback을 props를 통해서 받는다.
 - state, lifecycle method, performance optimization 필요하지 않기때문에 functional components로 작성된다.

## Container Components
 - 화면이 동작하는 것에 관심을 갖는다.
 - wrapping divs 를 제외하고는 DOM 마크업을 갖고 있지 않으며, 어떠한 style 관련 코드도 없다.
 - State 및 행위들을 presentational or container 에 제공한다.
 - Redux Actions 을 호출하는 코드가 삽입된다.
 - Redux의 connect()를 사용한다.

## Presentational 과 Container를 분리하는 것의 장점
 - seperation of concern 을 통해 app을 이해하기가 더 쉬워진다.
 - Better reusability
    - P.Component를 완전히 다른 State를 사용하는 다른 소스에 사용할 수 있다. 
 - Designer 작업시 P.Component만 보면 되므로 작업하기가 더 쉽다(로직이 없으므로)

## 
- P.Component 먼저 작읍을 하라.
    

## Container Components
- [React Components](https://medium.com/@learnreact/container-components-c0e67432e005#.dizbxjiyl)
- [Presentational and Container Components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)