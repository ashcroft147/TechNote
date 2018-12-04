## Namespaces
- internal modules 라고 표현하며 결국 global scope에 등록된 정리 안된 코드들을 namespace 키워드를 사용해서 Javascript Object 묶어서 관리하며 캡슐화를 하는 것을 의미한다. 
- namespace 내에 export 키워드를 사용하여 외부에 노출하고자 하는 function을 등록한다. 
- global scope에 무분별한 function의 등록을 방지한다. 
- 서로 다른 파일에 동일한 namespace를 등록할 수 있다. 
- Module Loader가 필요하지 않다.

mathCircle.ts
~~~
namespace Math {
    export function circle() {

    }
}
~~~

mathRectangle.ts
~~~
namespace Math {
    export function rectangle() {
        
    }
}
~~~

### Namespace 사용
namespace는 한개의 파일내에서 namespace 이름으로 참조할 수 있다. 
만약 외부파일에 존재하는 namespace를 참조하는 경우에는 다음과 같이 참조한다. 

~~~
/// <reference path="mathCircle.ts" />
~~~

### nested namespace
namepace 내에 namespace를 정의할 수 있다. 

~~~
namespace Math {
    export namespace Circle {
        export function circle() {

        }
    }
}
~~~

위와 같이 정의되었을때 circle함수에 대한 접근은 다음과 같이 할 수 있다. 

~~~
Math.Circle.circle();
~~~

## Modules ?
- Typescript에서 모듈이란 ts 혹은 js 파일 최상단에 import 혹은 export 되는 파일들을 의미한다. 
- namepace와는 달리 real module을 사용해서 코드를 organize 할 수 있다. 
- browser에서는 module loader 가 아직 지원이 되지 않으므로 module loader가 필요하다.

## Export
- 선언적으로 사용되는 variable, function, class, type alias, or interface는 export 키워드를 앞에 붙여서 모듈로 만들 수 있다.

### Default Exports
- default 키워드를 붙이면 default exports를 선언하는 것이며, 각 모듈당 한개씩만 선언할 수 있다. 
- default export는 서로 다른 form으로 import가 되는데 * 를 사용하지 않는다.

## Namespace vs Module
사용법의 차이
 - namespace는 namespace 키워드를 사용하고, namespace 내의 export 키워드가 사용된 함수나 상수에 대한 참조를 할 수 있다. 
    - 다른 파일에 대한 참조는 reference를 사용
 - module은 다른 파일에 export 키워드로 정의한 내용을 import 키워드로 불러와서 사용한다.

<B>참조 링크</B>
- [Modules from Typescript Doc](https://www.typescriptlang.org/docs/handbook/modules.html)
- [Namespaces from Typescript Doc](https://www.typescriptlang.org/docs/handbook/namespaces.html)