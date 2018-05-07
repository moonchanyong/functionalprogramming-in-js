
# es5 versus es6

** es와 es5의 경계없이 사용해서 경계만들기 위해서 차이 공부 **

* 2015년 6월 ES6 최종 스팩이 승인되어 크롬과 파이어폭스에서는 쉽게 ES6 을 사용할 수 있지만 다른 브라우저는 babel, traceur, es6-shim(transpiling tool)등을 이용해야 한다.

## 변수형 추가

* var 5에서 const와 let 추가

## module import

* es5에서는 require를 사용했으나, 이제는 import를 사용한다.

## class define

    // es5
    function pizza(size, topping){
      this.size = size;
      this.topping = topping;
    }

    pizza.prototype.eat = function() {
      return "yamyam";
    }

    // es6 typescript 문법인줄알앗네 이거 ;
    class pizza {
      constructor(size, topping) {
        this.size = size;
        this.topping = topping;
      }

      eat() {
        return "yamyam";
      }
    }

## Inheritance

    // es5
    var component = pizza.createClass()

    // es6
    class component extends pizza {}


## arrow function expression

    // es5
    [1, 2, 3].foreach(function(){});

    // es6
    [1, 2, 3].foreach()() => {});
