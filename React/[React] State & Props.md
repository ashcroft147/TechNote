## props
 - 컴포넌트 사용 할 데이터중 변동되지 않는(immutable) 데이터에 사용
 - parent 에서 child component로 데이터를 전달할 때 props 사용
 - 사용방법
    - parent
        - ReactDOM.render(reactElement, DOMElement) 에서 reactElement render 시에 속성 및 값을 정의(<> 안에 정의)
        - ReactDOM.render(<App headerTitle = "Welcome!", contentTitle = "Stranger,"
                     contentBody = "Welcome to example app"/>, document.getElementById('app')); 
    - child: render() 메소드 내에서 {this.props.propsName} 형식으로 props의 값을 받아서 사용
    ~~~
    class Content extends React.Component {
        render(){
            return (
                <div>
                    <h2>{ this.props.title }</h2>
                    <p> { this.props.body } </p>
                </div>
            );
        }
    }
    ~~~
 - 기본 값 설정하기
    - Component 클래스 하단에 className.defaultProps = {propName: value} 를 삽입한다.
    ~~~
    App.defaultProps = {
        headerTitle: 'Default header',
        contentTitle: 'Default contentTitle',
        contentBody: 'Default contentBody'
    };
    
    ReactDOM.render(<App />, document.getElementById('app'));
    ~~~
- Type Validation
    - child Component에서 원하는 props의 type을 지정하여 원하는 type이 아닌경우 콘솔에서 오류 메시지가 나오게 할 수 있다. 
    - propTypes 객체 설정
    
    ~~~
    import React from 'react';
 
    class Content extends React.Component {
        render(){
            return (
                <div>
                    <h2>{ this.props.title }</h2>
                    <p> { this.props.body } </p>
                </div>
            );
        }
    }
    
    Content.propTypes = {
        title: React.PropTypes.string,
        body: React.PropTypes.string.isRequired // 필수 지정
    };
    
    export default Content;

    // JS primitive types
    optionalArray: React.PropTypes.array,
    optionalBool: React.PropTypes.bool,
    optionalFunc: React.PropTypes.func,
    optionalNumber: React.PropTypes.number,
    optionalObject: React.PropTypes.object,
    optionalString: React.PropTypes.string,
    ~~~

## State
 - 컴포넌트에서 유동적인 데이터를 다룰때 사용한다. 
 - state를 사용하는 Component의 갯수는 최소화 해야 한다. why?
 - container component를 만든 후 나머지는 props를 통해 데이터를 전달하도록 설계해야 한다.
 - 사용법
    - state 의 초기 값을 설정 할 때는 constructor(생성자) 메소드에서 this.state= { } 를 통하여 설정합니다.
    - state 를 렌더링 할 때는 { this.state.stateName } 을 사용합니다.
    - state 를 업데이트 할 때는 this.setState() 메소드를 사용합니다. ES6 class에선 auto binding(what ?)이 되지 않으므로, setState 메소드를 사용 하게 될 메소드를 bind 해주어야 합니다. (bind 하지 않으면 React Component 가 가지고있는 멤버 함수 및 객체에 접근 할 수 없습니다.)
 - 예제코드
    - App.js
    ~~~
    import React from 'react';
    import ReactDOM from 'react-dom';
    import Header from './Header';
    import Content from './Content';
    import RandomNumber from './RandomNumber';
    
    class App extends React.Component {
    
        constructor(props){
            super(props);
    
            this.state = {
                value: Math.round(Math.random()*100)
            };
    
            this._updateValue = this._updateValue.bind(this);
        }
    
        _updateValue(randomValue){
            this.setState({
                value: randomValue
            });
        }
    
        render(){
            return  (
                <div>
                    <Header title={ this.props.headerTitle }/>
                    <Content title={ this.props.contentTitle }
                            body={ this.props.contentBody }/>
                        <RandomNumber number={this.state.value}
                                    onUpdate={this._updateValue} />
                </div>
            );
        }
    }
    
    App.defaultProps = {
        headerTitle: 'Default header',
        contentTitle: 'Default contentTitle',
        contentBody: 'Default contentBody'
    };
    
    ReactDOM.render(<App/>, document.getElementById('root'));
    ~~~

    - RandomNumber.js  
    ~~~
    
    import React from 'react';
    import ReactDOM from 'react-dom';
    
    
    class RandomNumber extends React.Component {
        _update(){
            let value = Math.round(Math.random()*100);
            this.props.onUpdate(value);
        }
    
        constructor(props){
            super(props);
            this._update = this._update.bind(this);
        }
    
        render(){
            return (
                <div>
                    <h1>RANDOM NUMBER: { this.props.number }</h1>
                    <button onClick={this._update}>Randomize</button>
                </div>
            );
        }
    }
    
    export default RandomNumber;
    ~~~
