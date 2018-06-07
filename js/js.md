
# es5 versus es6

** es와 es5의 경계없이 사용해서 경계만들기 위해서 차이 공부 **

* 2015년 6월 ES6 최종 스팩이 승인되어 크롬과 파이어폭스에서는 쉽게 ES6 을 사용할 수 있지만 다른 브라우저는 babel, traceur, es6-shim(transpiling tool)등을 이용해야 한다.

## JS 이해하기

### scope
* C 같은 경우는 block scope
    + if 문 등 따로 scope가 주어진다.
* 자바 스크립트는 function scope를 사용
    + if 내에서는 scope가 따로 주어지지 않음
### Lexical

* 다른 말로 static 이라고도 이해한다고 한다.


### js의 함수는 1급 객체이다

#### 1급 객체란(first class object)

##### 1급시민의 정의 (first class citizen)
*** 대부분의 언어는 조건 충족 ***
* 변수(variable)에 담을 수 있다
* 인자(parameter)로 전달할 수 있다
* 반환값(return value)으로 전달할 수 있다


#### 1급 객체는 1급시민의 정의를 만족하는 객체
* 객체를 1급 시민으로 취급

#### 1급함수 (first class function)

* 함수를 1급시민으로 취급
* 1급시민의 정의를 충족
* 몇몇학자는 추가로 두가지 더 요구한다고 한다
    + 런타임 생성이 가능하다(동적언어의 특성으로 자바는 동적으로 객체를 생성하는 듯이 보이지만 리퍼렌스타입으로 변수가 미리 선언되있다. 자바같은경우 바이트코드를 조작해야 가능, 어렵다고한다.)
    + 익명으로 생성이 가능하다

*** 추가조건으로 인해 C언어는 불가능 하다. ***

### first class function이 중요한이유

#### 함수를 주고받고 핸들링이 가능하다는 말이다.

* 이를통해 고차함수가 가능하다
* 함수형 프로그래밍에 유용
    + 1급 객체가 클로저와 만나서 가능
    + JavaScript의 함수는 생성될 당시의 Lexical Environment를 기억한다. 함수를 주고받게 되면 이 Lexical Environment도 함께 전달된다. (closure 이유인듯)
    + 커링(currying)과 메모이제이션(memoization)이 가능해진다.

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
    + var keyword
      - Function Scope
      - Hoisting
      - 중복선언 가능
    + let keyword
      - block Scope
      - no Hoisting
      - 중복선언 불가(에러 발생)


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


# JSModule

## Uglify
* 코드를 미니멀리즘화 하는 모듈이다.
(코드의 가독성을 위한 띄어쓰기 줄바꿈 같은등을 제거해주는 npm 모듈이다.)
(최적화를 위해 사용하는 모듈)

## Polyfill

* 폴리필(polyfill)은 개발자가 특정 기능이 지원되지 않는 브라우저를 위해 사용할 수 있는 코드 조각이나 플러그인을 말한다. 폴리필은 HTML5 및 CSS3와 오래된 브라우저 사이의 간격을 메꾸는 역할을 담당한다.

## CommonJs 와 AM

* 두개 비교의 이유는 JavaScript 모듈화 작업의 선두 주자
* webpack을 쓰면 동시에 지원 된다고 한다.
### CommonJs

CommonJS(http://www.commonjs.org/) 는 JavaScript를 브라우저에서뿐만 아니라, 서버사이드 애플리케이션이나 데스크톱 애플리케이션에서도 사용하려고 조직한 자발적 워킹 그룹이다.
* JavaScript를 브라우저에서만 사용하는 언어가 아닌 일반적인 범용 언어로 사용할 수 있도록 하겠다는 의지

##### 핵심은 모듈화
CommonJS의 주요 명세는 바로 이 모듈을 어떻게 정의하고, 어떻게 사용할 것인가에 대한 것이다.

*** 모듈화  ***

* 스코프(Scope): 모든 모듈은 자신만의 독립적인 실행 영역이 있어야 한다.
* 정의(Definition): 모듈 정의는 exports 객체를 이용한다.
* 사용(Usage): 모듈 사용은 require 함수를 이용한다.

 CommonJS의 모듈 명세는 모든 파일이 로컬 디스크에 있어 필요할 때 바로 불러올 수 있는 상황을 전제로 한다. => 서버사이드 javascript 환경을 전제로 한다

필요한 모듈을 다운 받을 때까 아무것도 할 수없는 단점이 있다. 그래서 동적으로 스크립트 태그를 삽입하는 방법을 쓴다(js 로더들 가장 많이사용하는 방법)

#### 비동기 모듈 로드 문제

* 자바스크립트가 브라우저에서 동작할때 서버사이드와 달리 파일 단위 스코프가없다
* 스크립트 태그를 이용해 로드하면 각 전역 스코프가 엉킬 가능성이 있다.

*** 이를 해결하기위한 모듈 전송 포맷(module transport format) ***
* 클로저를 통해 전역변수 통제한다

전송 포맷으로 감싸면 서버 모듈을 비동기적으로 로드할 수 있게 된다.
    // complex-numbers/plus-two.js

    require.define({"complex-numbers/plus-two": function(require, exports){

        //콜백 함수 안에 모듈을 정의한다.
        var sum = require("./complex-number").sum;  
        exports.plusTwo = function(a){  
          return sum(a, 2);  
        };
    },["complex-numbers/math"]);
    //먼저 로드되어야 할 모듈을 기술한다.

### AMD(Asynchronous Module Definition)
* AMD 그룹은 비동기 상황에서도 JavaScript 모듈을 쓰기 위해 CommonJS에서 함께 논의하다 합의점을 이루지 못하고 독립한 그룹이다.

* CommonJS가 JavaScript를 브라우저 밖으로 꺼내기 위한 노력의 일환
* AMD는 브라우저 내의 실행을 중점으로 두엇다.

AMD 만의 특징

대표적으로 꼽을 수 있는 것이 바로 define() 함수다. 브라우저 환경의 JavaScript는 파일 스코프가 따로 존재하지 않기 때문에 이 define() 함수로 파일 스코프의 역할을 대신한다. 즉, 일종의 네임스페이스 역할을 하여 모듈에서 사용하는 변수와 전역변수를 분리한다. 물론 define() 함수는 전역함수로 AMD 명세를 구현하는 서드파티 벤더가 모듈 로더에 구현해야 한다.


* AMD 모듈 명세의 장점은 단연 비동기 환경에서도 매우 잘 동작할 뿐만 아니라, 서버사이드에서도 동일한 코드로 동작한다는 점
* CommonJS의 모듈 전송 포맷보다는 확실히 간단하고 명확하다.

* AMD 명세는 define() 함수(클로저를 이용한 모듈 패턴)를 이용해 모듈을 구현하므로 전역변수 문제가 없다.
* Lazy-Load 기법을 응용할 수도 있다.
