## Interface
 - Blueprint of Function
 - Function이 가지는 Parameter의 타입을 정의할 수 있다
 ~~~
 interface operateInterface {
     shape:string;
     side?:number;
 }

 function operate(x:operateInterface) {
     return x.side*x.side;
 }

 var calc = operate({shape:"square", side:5})
 ~~~

 ~~~
 interface player {
     run(): void;
     addLives(n:number): void;
     score():number;
 }

function createPlayer():player {
    return {
        run: function() {},
        addLives: function(n:number) {},
        score: function() {return 1}
    }
}

var player1 = createPlayer();

 ~~~