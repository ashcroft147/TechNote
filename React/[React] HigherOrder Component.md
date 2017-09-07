## Higher Order Component ?
React Component that adds some additional functionality or behavior to an exsiting component that you've already written or planned to write in the future

Component + Higher Order Component = Enhanced or Composed Component

It is also great for providing duplicate logic all over the place inside of our app

react-redux is a kind of Higher Order Component

Common Pattern
~~~
export default connect(mapStateToProps)(App);
~~~