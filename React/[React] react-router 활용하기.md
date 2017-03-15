# Container Component Pattern
> A container does data fetching and then renders its corresponding sub-component.
  react-router에 의해서 routing되는 component
 - data fetching: state 변화에 따른 데이터를 가져오는 행위
 - corresponding: 동일한 이름을 공유하는 Component
   (tockWidgetContainer => StockWidget)

## CommentList Component
 - data fetching과 data를 presenting하는 코드가 같은 Component에 있는데 React의 장점들을 살리지 못함 
~~~
// CommentList.js
class CommentList extends React.Component {
  constructor() {
    super();
    this.state = { comments: [] }
  }
  componentDidMount() {
    $.ajax({
      url: "/my-comments.json",
      dataType: 'json',
      success: function(comments) {
        this.setState({comments: comments});
      }.bind(this)
    });
  }
  render() {
    return <ul> {this.state.comments.map(renderComment)} </ul>;
  }
  renderComment({body, author}) {
    return <li>{body}—{author}</li>;
  }
}
~~~

## CommentListContainer
 - data fetching
~~~
// CommentListContainer.js
class CommentListContainer extends React.Component {
  constructor() {
    super();
    this.state = { comments: [] }
  }
  componentDidMount() {
    $.ajax({
      url: "/my-comments.json",
      dataType: 'json',
      success: function(comments) {
        this.setState({comments: comments});
      }.bind(this)
    });
  }
  render() {
    return <CommentList comments={this.state.comments} />;
  }
}
~~~

## CommentList
 - data presenting
~~~
// CommentList.js
class CommentList extends React.Component {
  constructor(props) {
    super(props);
  }
  render() { 
    return <ul> {this.props.comments.map(renderComment)} </ul>;
  }
  renderComment({body, author}) {
    return <li>{body}—{author}</li>;
  }
}
~~~

# react-router
 - 사용자가 요청한 URL에 따라서 서로다른 화면을 Rendering 한다. 
 - Router를 사용하면 처음부터 웹앱에 사용할 모든 Component들을 먼저 불러와두고, 
   페이지를 처음부터 로딩하는것이 아닌 필요한 컴포넌트만 렌더링 한다. 

## react-router 설치
~~~
$ npm install --save react-router
~~~

## component 종류
### IndexRoute
 > IndexRoute: /에 해당하는 path에 기본으로 보이는 Children 컴포넌트를 설정.
   IndexRoute에 지정된 컴포넌트는 this.props.children 속성으로 App 컴포넌트에 전달됩니다.
 - this.props.children = undefined
~~~
<Router>
  <Route path="/" component={App}>
    <Route path="accounts" component={Accounts}/>
    <Route path="statements" component={Statements}/>
  </Route>
</Router>
~~~

 - this.props.children = Home
~~~
<Router>
  <Route path="/" component={App}>
    <IndexRoute component={Home}/>
    <Route path="accounts" component={Accounts}/>
    <Route path="statements" component={Statements}/>
  </Route>
</Router>
~~~

## IndexRedirect
 - 다음의 route 셋업에서, /를 /accounts 로 redirect 하고 싶은 경우, IndexRedirect component를 사용해서 redirect을 할 수 있다. 
~~~
<Router>
  <Route path="/" component={App}>
    <Route path="accounts" component={Accounts}/>
    <Route path="statements" component={Statements}/>
  </Route>
</Router>
~~~

 - redirect to Accounts component
~~~
<Router>
  <Route path="/" component={App}>
    <IndexRedirect to="/accounts"/>
    <Route path="accounts" component={Accounts}/>
    <Route path="statements" component={Statements}/>
  </Route>
</Router>
~~~

##

 - Route: 페이지가 늘어날 때마다 컴포넌트를 만든 후 Route에 추가

## Reference
 1. [Container Components](https://medium.com/@learnreact/container-components-c0e67432e005#.t0i0iwdl0)
 1. [velopert](https://velopert.com/2937)
 1. [Github: react-router](https://github.com/ReactTraining/react-router/tree/v3/docs/)