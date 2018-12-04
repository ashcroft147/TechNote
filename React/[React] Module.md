## export
- export는 function, object, constants를 외부로 연결할 때 사용한다. 


## Named export
 - export 하는 func 의 네임과 import 하는 func의 네임은 동일해야 한다.
 - 한개의 module에 여러개의 export가 있을 수 있다.
named_export.js
~~~
export function func() {

}

export function func1() {

}
~~~

named_import.js
~~~
import { func, func1 } from './named_export';
~~~

## Default export
- 한개 파일에는 한개의 default export 만 있을 수 있다. 
- module import 시 named 와 default는 동시에 import 될 수 있다.
- default export 된 module의 name은 export module의 네임과 동일하지 않아도 된다.
default_export.js
~~~

~~~

default_import.js
~~~
import defaultExport, { namedExport1, namedExport3, etc... } from 'module';
~~~
