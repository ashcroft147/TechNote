## refs
  > React의 일반적인 dataflow에서 parent components와 children components가 데이터를 주고 받는 유일한 방법은 props를 통해서 이다. 하지만 어떨때는 일반적인 data의 흐름을 통하지 않고 데이터를 변경해야 하는 경우가 있는데, 이때 refs를 사용할 수 있다.

1. Use Cases
  - Component 자신에 의해 Rendor된 DOM에 직접 어떠한 처리를 하는 경우
    - focus, text선택, media의 playback
    - Animation 을 작동시키는 경우
  - third-party DOM 라이브러리를 병합하는 경우

2. 사용시 유의점
 - state, props로 해결할 수 있는 부분은 ref를 사용하지 않는다.
 
3. DOM Element에 Ref 사용하기
~~~
import React from 'react';

class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    this.focus = this.focus.bind(this);
  }

  focus() {
    // Explicitly focus the text input using the raw DOM API
	debugger;
    this.textInput.focus();
  }

  render() {
    // Use the `ref` callback to store a reference to the text input DOM
    // input -> 사용자 입력, this.textInput -> Input Dom Element을 가리키는 참조변수로 사용
    // element in an instance field (for example, this.textInput).
    return (
      <div>
        <input
          type="text"
          ref={(input) => { this.textInput = input; }} /> 
        <input
          type="button"
          value="Focus the text input"
          onClick={this.focus}
        />
      </div>
    );
  }
}

export default CustomTextInput;
~~~
4. Class Component 에 Ref 사용하기
- ref는 DOM요소 뿐만 아니라 컴포넌트에 사용해서 컴포넌트의 내장 메소드 및 변수를 사용할 수 있다.
~~~
~~~

5. Functional Components 에 Ref 사용하기



---
 - 사용
 ~~~
 class Hello extends React.Component {
  render() {
   return (
       <div> 
           <input ref={ref => this.input = ref}>
            </input>
          </div>
        )
  }
  
  componentDidMount() {
   this.input.value = "I used ref to do this";
  }
}

ReactDOM.render(
  <Hello/>,
  document.getElementById('app')
);
 ~~~