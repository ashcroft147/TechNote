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

### Pure Component
React.PureComponent는 ShouldComonentUpdate API를 제외하고는 React.Component와 동일하다
PureComponent는 shallow-compare를 수행하여 기본적으로 Reconcilation을 수행하지 않고 ShouldComonentUpdate의 구현체가 없으므로 작성하지 않아야 한다. 
~~
//...
if (instance.shouldComponentUpdate) {
  shouldUpdate = instance.shouldComponentUpdate(nextProps, nextState, nextContext);
} else if (instance.isPureComponent) {
  // PureComponent는 shouldComponentUpdate의 구현체가 없고 renderer에서 직접 shallow-compare를 수행한다.
  shouldUpdate = (
    !shallowEqual(prevProps, nextProps) || 
    !shallowEqual(instance.state, nextState)
  );
}
//...

return shouldUpdate;
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


## 참고자료
 - [React 렌더링과 성능 알아보기](http://meetup.toast.com/posts/110)
 - [React Components, Elements, and Instances](https://medium.com/@dan_abramov/react-components-elements-and-instances-90800811f8ca)