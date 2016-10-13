## Default Parameters
- Javascript에서는 파라미터는 optional하며, 함수호출시 생략될 수 있으며 그러한 경우에 
파라미터의 값은 undefined가 된다. 
- Typescript는 함수 호출시 모든 파라미터에 값이 할당되었는지 compiler가 체크를 한다. 
- 즉, Parameter의 갯수와, Argument의 갯수는 동일해야 한다.
~~~
function buildName(firstName: string, lastName: string) {
    return firstName + " " + lastName;
}

let result1 = buildName("Bob");                  // error, too few parameters
let result2 = buildName("Bob", "Adams", "Sr.");  // error, too many parameters
let result3 = buildName("Bob", "Adams");         // ah, just right
~~~


## Default-initialized Parameters
- Typescript에서 초기화되는 파라미터는 Optional Paramter와 동일하다.
- 초기화 파라미터에 undefined를 할당하거나, 아무 Argument도 할당하지 않으면 초기화를 실행한다.
~~~
function buildName(firstName: string, lastName = "Smith") {
    return firstName + " " + lastName;
}

let result1 = buildName("Bob");                  // works correctly now, returns "Bob Smith"
let result2 = buildName("Bob", undefined);       // still works, also returns "Bob Smith"
let result3 = buildName("Bob", "Adams", "Sr.");  // error, too many parameters
let result4 = buildName("Bob", "Adams");         // ah, just right
~~~

## Optional Parameters
- Typescript에서 파라미터 뒤에 ?를 둠으로써, Optional Parameter를 정의해 사용할 수 있다.
~~~
function buildName(firstName: string, lastName?: string) {
    if (lastName)
        return firstName + " " + lastName;
    else
        return firstName;
}

let result1 = buildName("Bob");                  // works correctly now
let result2 = buildName("Bob", "Adams", "Sr.");  // error, too many parameters
let result3 = buildName("Bob", "Adams");         // ah, just right
~~~