
# es5 versus es6

** es와 es5의 경계없이 사용해서 경계만들기 위해서 차이 공부 **

* 2015년 6월 ES6 최종 스팩이 승인되어 크롬과 파이어폭스에서는 쉽게 ES6 을 사용할 수 있지만 다른 브라우저는 babel, traceur, es6-shim(transpiling tool)등을 이용해야 한다.

## JS 이해하기

### ECMAScript 가 생긴이유

* 웹브라우져의 통일을 위한 표준 규격
* ECMA 국제 기구에서 “ECMAScript Standard” 표준규격을 정함
* Javascript는 ECMAScript와 BOM(Browser Object Model) 와 DOM(Document Object Model)이라는 1개의 코어와, 2개의 모델로 이루어져 있다.

### ECMAScript


* ECMAScript는 자바 스크립트를 이루는 코어(Core) 스크립트 언어
* 웹 환경에서만 호스트 되는 언어가 아니다. 웹 환경은 ECMA 스크립트가 호스트되는 환경들 중 하나(백엔드, 펌웨어 등)
* ECMA 스크립트 호스트 환경은 ECMA 스크립트 실행 환경이 구현되있고, 각각 그 환경에 알맞는 확장성을 가지고 있다.


출처: http://takeuu.tistory.com/93 [워너비스페셜]



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
    [1, 2, 3].foraEach(function(){});

    // es6
    [1, 2, 3].forEach()() => {});


## template literals

*** es6에만 추가 ***

    // 백틱
    `string text ${expression} string text`

### Nesting templates

    // Nesting templates 사용 안 한 경우
    const classes = `header ${ isLargeScreen() ? '' :
    (item.isCollapsed ? 'icon-expander' : 'icon-collapser') }`;

    // Nesting templates 사용
    const classes = `header ${ isLargeScreen() ? '' :
    `icon-${item.isCollapsed ? 'expander' : 'collapser'}` }`;

### Tagged templates


    tag = (strings, a, b) => strings + a + b;

    console.log(tag`pizza ${zzang} ${zzang}`);
