## ref
 - reference를 의미하며, DOM 요소에 이름을 달아준다.
 - state, props로 해결할 수 있는 부분은 ref를 사용하지 않는다. 
 - ref를 사용하는 경우
    - Component 에 의해 Rendor된 DOM에 직접 어떠한 처리를 하는 경우
    - 다른 F/W와 혼용해서 큰 프로젝트에 React를 사용하는 경우
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