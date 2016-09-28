## TypeScript란
 - TypeScript는 컴파일하면 Javascript가 되는(Compile-to-Javascript) 언어이다. 컴파일 시점에 타입을 체크하고 전통적인 객체지향 프로그래밍 패턴을 도입한다. 


## TypeScript의 설치
 - npm을 사용해서 설치
 - 설치가 완료되면 tsc 명령어를 command line에서 실행시켜본다.
 ~~~
 npm install -g typescript 
 ~~~

## TypeScirpt Compile
~~~
tsc helloworld.ts
~~~

## TypeScript 개발에 사용하는 패키지
 - Typings – typings.json에 설정을 통해 TypeScirpt definitions()를 설치하고 유지관리하는 단순한 방법을 제공한다. 상세한 사용법은 여기를 클릭 한다.
 - tsify – tsconfig.json 설정을 통해, TypeScript 로 작성된 코드를 컴파일 하기위해 사용하는 패키지 이다. 상세한 사용법은 여기를 클릭 한다.
~~~
browserify playground.ts -p [tsify] | uglifyjs -c > dist/bundle.js
~~~

## TypeScript의 장점
 - 자바스크립트 사용시 타입 체크를 위한 코드나 테스트를 작성하지 않아도 된다. 
 - 컴파일 타임 타입 체크를 해준다. 
 - ES6의 기능들을 사용할 수 있다. (클래스)