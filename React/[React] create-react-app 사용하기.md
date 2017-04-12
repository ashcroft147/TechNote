# create-react-app 을 사용한 react project template 생성

## create-react-app 설치
~~~
$ npm install -g create-react-app
~~~
 - Globally 패키지를 설치한다. 그리고 Node 버전은 4.x 이상이어야 한다.
 - We strongly recommend to use Node >= 6 and npm >= 3 for faster installation speed and better disk usage.

## App 생성
 - 우선, create-react-app을 통해 프로젝트를 생성하고자 하는 프로젝트의 root directory로 이동
 - 다음의 명령어를 실행하면, my-app 프로젝트가 생성된다. 
 ~~~
 $ create-react-app my-app
 $ cd my-app
 ~~~

## 서버 실행
~~~
$ npm start
~~~
- webpack-dev-server를 시작할 수 있다.
- hot-reload가 적용되어 있어 코드 수정하면 서버는 자동으로 재실행 된다.
- ESLint를 통하여 경고 메시지를 콘솔에 출력해준다.

## 빌드
~~~
$ npm run build
~~~
- 위 명령어를 통하여 빌드를 수행한다. 
- code의 minify 및 envify가 수행된다.


