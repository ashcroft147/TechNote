## Components
> render 메소드를 포함하는 Class or Function
 - component는 세가지 방식으로 정의할 수 있다.
    - functions
        - single render method만 가진다.
        - local state를 가질수 없다.
    ~~~
    const Button = ({params}) => {
        ...
    };
    ~~~
    - class with React.createClass
    ~~~
    const Button = React.createClass({
        ...
    });
    ~~~
    - class with React.Component(ES6 Style)
    ~~~
    class Button extends React.Component {
        ...
    }
    ~~~


## Elements
 - DOM node를 설명하는 plain object를 나타낸다. 
 ~~~
 <button class='button button-blue'>
  <b>
    OK!
  </b>
</button>
 ~~~

### Component Elements
- element의 type이 function 혹은 React class로 표현한 것을 의미한다.
~~~
const DangerButton = ({ children }) => ({
  type: Button,
  props: {
    color: 'red',
    children: children
  }
});
~~~

## Instances
> component 클래스 안에서 this로 참조하는 객체들을 instance라고 한다. 