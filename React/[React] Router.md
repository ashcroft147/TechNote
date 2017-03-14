# Container Component Pattern
> A container does data fetching and then renders its corresponding sub-component.
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


## Router
 - Router를 사용하면 처음부터 웹앱에 사용할 모든 Component들을 먼저 불러와두고, 
   페이지를 처음부터 로딩하는것이 아닌 필요한 컴포넌트만 렌더링 한다. 

## Reference
 [Container Components](https://medium.com/@learnreact/container-components-c0e67432e005#.t0i0iwdl0)