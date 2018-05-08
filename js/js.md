
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

### closure
* 컴퓨터 언어에서 클로저(Closure)는 일급 객체 함수(first-class functions)의 개념을 이용하여 스코프(scope)에 묶인 변수를 바인딩 하기 위한 일종의 기술
* 기능상으로, 클로저는 함수를 저장한 레코드(record)이며, 스코프(scope)의 인수(Factor)들은 클로저가 만들어질 때 정의(define)되며, 스코프 내의 영역이 소멸(remove)되었어도 그에 대한 접근(access)은 독립된 복사본인 클로저(return 된)를 통해 이루어질 수 있다.

*** 코드를 보는것이 빠르다 ***

    function startAt(x){
        function incrementBy(y){
            return x + y;
        }
        return incrementBy;
    }

    var closure1 = startAt(1);
    closure1(1); // return 2
    var closure2 = startAt(2)
    closure2(1); // return 3

### hoisting

*  변수의 정의가 그 범위에 따라 선언과 할당으로 분리 됨
* 함수도 마찬가지
* 코드 상단에서 초기화 스타일을 추천함


    function showName() {
      console.log("First Name : " + name);
      var name = "Ford";
      console.log("Last Name : " + name);
    }
    showName();
    // First Name : undefined
    // Last Name : Ford
    // First Name이 undefined인 이유는 지역변수 name이 호이스트 되었기 때문입니다.


    // 엔진에서 해석 된 코드
    var showName;
    function showName() {
      var name; // name 변수는 호이스트 되었습니다. 할당은 이후에 발생하기 때문에, 이 시점에 name의 값은 undefined 입니다.
      console.log("First name : " + name); // First Name : undefined
      name = "Ford"; // name에 값이 할당 되었습니다.
      console.log("Last Name : " + name); // Last Name : Ford
    }

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
    // 클래스는 호이스팅이 지원 안된다.
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

## for of

* es6에서 추가 된 문법 for of
* es5의 for in의 문제점은 object를 위해 나와서 배열에서 문제
    + 프로토 타입 체인도 순회
    + 순서가 무작위
    + index가 string

* es6부터 배열을 순회하려면 for of을 사용하면 된다.
* 객체는 for in을 사용


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
