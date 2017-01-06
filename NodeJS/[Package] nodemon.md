## nodemon ?
nodemon은 프로젝트 폴더의 파일들을 모니터링하고 있다가 <B>파일이 수정되면 자동으로 서버를 Restart 시켜준다. </B>

## nodemon 설치
~~~
$ npm install nodemon -g
~~~

## nodemon 사용하기
 - node 실행방법
 ~~~
 $ node app.js
 ~~~
 - nodemon 실행방법
 ~~~
 $ nodemon app.js
 $ nodemon --delay 10 app.js // 파일 수정 후 10초 후 Restart
 ~~~

## 모니터링 파일 ignore
nodemon의 변화감지 대상에서 제외하고자 할 경우에 .nodemonignore파일을 프로젝트에 생성해 무시할 파일이나 디렉토리
작성


<B>참조 링크</B>

- [node.js 소스 수정시 자동으로 서버를 재시작 해주는 nodemon](https://blog.outsider.ne.kr/649)
- [npm nodemon documnet](https://www.npmjs.com/package/nodemon)