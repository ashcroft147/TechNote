### Arrow function은 non-methoed 함수를 표현하는데 적합하다.

### Arrow function doesn't create of this context
~~~
'use strict';
var obj = {
  i: 10,
  b: () => console.log(this.i, this),
  c: function() {
    console.log(this.i, this);
  }
}
obj.b(); // prints undefined, Object {...}
obj.c(); // prints 10, Object {...}
~~~

### Use of the new operator
Arrow function은 생성자로 사용될 수 없으며 new 키워드를 사용하면 Error를 던진다.
~~~
var Foo = () => {};
var foo = new Foo(); // TypeError: Foo is not a constructor
~~~

### Arrow function의 만들어진 목적
- shorter function
~~~
var materials = [
  'Hydrogen',
  'Helium',
  'Lithium',
  'Beryllium'
];

materials.map(function(material) { 
  return material.length; 
}); // [8, 6, 7, 9]

materials.map((material) => {
  return material.length;
}); // [8, 6, 7, 9]

materials.map(material => material.length); // [8, 6, 7, 9]
~~~

- non-binding of this 의 필요성
~~~
function Person() {
  // The Person() constructor defines `this` as an instance of itself.
  this.age = 0;

  setInterval(function growUp() {
    // In non-strict mode, the growUp() function 'this' 
    // as the global object, which is different from the `this`
    // defined by the Person() constructor.
    this.age++;
  }, 1000);
}

var p = new Person();
~~~

ES3, ES5에서 위와 같은 문제 해결을 위해 Person의 this object를 변수에 할당하여 사용하면서 해결
~~~
function Person() {
  var that = this;
  that.age = 0;

  setInterval(function growUp() {
    // The callback refers to the `that` variable of which
    // the value is the expected object.
    that.age++;
  }, 1000);
}
~~~ 

ES6 arrow function의 사용
~~~
function Person(){
  this.age = 0;

  setInterval(() => {
    this.age++; // |this| properly refers to the person object
  }, 1000);
}

var p = new Person();
~~~


### 참고자료
[arrow function](https://hacks.mozilla.org/2015/06/es6-in-depth-arrow-functions/)