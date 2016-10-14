## Class

- TypeScript
~~~
class website {
    url:string;
    facebookLikes:number;
}

var google = new website();

google.url = "http://google.com";
google.facebookLikes = 123;
~~~

- JavaScript
    - 결국 Javascript의 Module 패턴으로 변환하는것이고, Javascript의 Prototypal Inheritance의 특성은 유지한다. 
~~~
var website = (function(){
    function website() {

    }
    return website;
})();

var google = new website();

google.url = "http://google.com";
google.facebookLikes = 123;
~~~

## constructor
 - TypeScript
~~~
class website {
    url:string;
    facebookLikes:number;

    constructor(url:string, fblikes:number) { // TypeScript의 생성자 키워드
        this.url = url;
        this.facebookLikes = fblikes;
    }
}

var google = new website( "http://google.com", 123);
~~~

- JavaScript
~~~
var website = (function(){
    function website(url, fblikes) {
        this.url = url;
        this.facebookLikes = fblikes;
    }
    return website;
})();

var google = new website("http://google.com", 123);

~~~

## Method
 - TypeScript
~~~
class website {
    url:string;
    facebookLikes:number;

    constructor(url:string, fblikes:number) { // TypeScript의 생성자 키워드
        this.url = url;
        this.facebookLikes = fblikes;
    }

    likesInk():string {
        return (this.facebookLikes/1000) +  'K';
    }
}

var google = new website( "http://google.com", 123);

console.log(google.likesInk());
~~~

 - JavaScript
~~~
var website = (function(){
    function website(url, fblikes) {
        this.url = url;
        this.facebookLikes = fblikes;
    }
    website.prototype.likesInk = function(){
        return (this.facebookLikes/1000) +  'K';
    }
    return website;
})();

var google = new website("http://google.com", 123);
console.log(google.likesInk());
~~~

## Accessors(Getter And Setter)
- getter/setter는 object의 memeber에 접근하는 방법이다. 
- TypeScript
~~~
class rectangle {
    l1:number;
    l2:number;

    constructor(l1:number, l2:number) {
        this.l1 = l1;
        this.l2 = l2;

    }

    get area() {
        return this.l1* thisl2;
    }

    set area(l1:number, l2:number) {
        
    }
}

var myAwesomeRect = new rectangle(10,20);
console.log(myAwesomeRect.area);
~~~

 - JavaScript
~~~
var rectangle = (function(){
    function rectangle(l1, l2) {
        this.l1 = l1;
        this.l2 = l2;
    }
    Object.defineProperty(rectangle.prototype, "area", {
        get: function() {
            return this.l1*this.l2;
        },
        enumerable:true,
        configurable: true
    });
    return rectangle;
})();

var myAwesomeRect = new rectangle(10,20);
console.log(myAwesomeRect.area);
~~~