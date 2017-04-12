## Redux란 ?
 - React에서 Flux 아키텍처를 편하게 사용할 수 있도록 해주는 라이브러리 이다.
    ![React - 01](../img/ReactJS/react1.png)

## 의존모듈 설치
1. redux: predictable state container for JS Apps
1. react-redux: redux의 사용을 편리하게 도와주는 모듈

## Middleware
1. redux-thunk
 - thunk를 사용함으로써 function을 return하는 action creator이다.
 - thunk를 통해 action의 dispatch를 delay 하거나, 특정 조건에 부합할때만 action을 dispatch 하도록 할 수 있다.(비동기 통신에 사용)
1. redux-promise
 - [redux-promise on github](https://github.com/acdlite/redux-promise)
1. redux-logger
 - [redux-logger on github](https://github.com/evgenyrodionov/redux-logger)


## 설치하기
~~~
npm install --save redux react-redux
~~~

## 참고자료
 - [Using with React Redux](http://redux.js.org/docs/basics/UsageWithReact.html)
<<<<<<< HEAD
 - [리덕스 패턴(Redux pattern)](https://www.zerocho.com/category/React/post/57b60e7fcfbef617003bf456)
 - [redux-thunk](https://www.npmjs.com/package/redux-thunk)
||||||| merged common ancestors
 - [리덕스 패턴(Redux pattern)](https://www.zerocho.com/category/React/post/57b60e7fcfbef617003bf456)
=======
 - [리덕스 패턴(Redux pattern)](https://www.zerocho.com/category/React/post/57b60e7fcfbef617003bf456)
 - [Hot Reloading](https://facebook.github.io/react-native/blog/2016/03/24/introducing-hot-reloading.html)
 - [Time travel debugging](http://bestalign.github.io/2015/10/27/redux-hot-reloading-and-time-travel-debugging/)
>>>>>>> 04064eed3f6d7b8e924c8cedffc557fc588ee956
