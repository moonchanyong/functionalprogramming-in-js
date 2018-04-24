# functionalprogramming-in-js
functional programming in js 정리

## functional programming language의 특성 

![Image what makes a language functional](
https://github.com/moonchanyong/functionalprogramming-in-js/blob/master/%E1%84%8B%E1%85%A5%E1%86%AB%E1%84%8B%E1%85%A5%E1%84%90%E1%85%B3%E1%86%A8%E1%84%89%E1%85%A5%E1%86%BC.png?raw=true)

* However, in the case of JavaScript, the functional features are somewhat hidden.
* 함수형 프로그래밍은 깨끗하고 단순하고 적고 디버깅과 테스팅과 유지보수에 좋다! (약장수급;;)

** imperative techniques

function merge2ArrayIntoOne (arrays) {

  var count = array.length;
  
  var c = 0;
  
  for (var j = 0, jlen = arrays[i].length; j < jlen; ++j) {
  
    merged[c++] = arrays[i][j];
    
  }
  
  return merged;
  
} 
** functional techniques (간단 인정)
varmerge2dArrayIntoOne2  = function(arrays) {
  return arrays.reduce ( function (p, n) {
    return p.concat(n);
  });
}
## Modularity 

코드는 모듈식으로 되서 테스트가 간단해진다 

## Reusability

모듈은 재사용성이 좋다 

## Reduced coupling
///////////
모듈간 의존성이 감소한다

전역변수에 side effects가 없고, 독립적이다 

## Mathematically correct

이 성질로 인해 올바르다는것이 증명된다. 

lazy execution strategy를 통해 필요한 숫자만 계산할 수 있다.

## 자바스크립트가 함수형 언어인 이유

* JavaScript's lexical grammar includes the ability to pass functions as
arguments, has an inferred type system, and allows for anonymous
functions, higher-order functions, closures and more. These facts
are paramount to achieving the structure and behavior of functional
programming

* It is not a pure object-oriented language, with most object-oriented design
patterns achieved by copying the Prototype object, a weak model for
object-oriented programming. European Computer Manufacturers
Association Script (ECMAScript), JavaScript's formal and standardized
specifications for implementation, states the following in specification 4.2.1:

> + "ECMAScript does not contain proper classes such as those in
C++, Smalltalk, or Java, but rather, supports constructors which
create objects. In a class-based object-oriented language, in general,
state is carried by instances, methods are carried by classes, and
inheritance is only of structure and behavior. In ECMAScript, the
state and methods are carried by objects, and structure, behavior
and state are all inherited."

* It is an interpreted language. Sometimes called "engines", JavaScript
interpreters often closely resemble Scheme interpreters. Both are dynamic,
both have flexible datatypes that easily combine and transform, both evaluate
the code into blocks of expressions, and both treat functions similarly.


# working with functions 

## Self-invoking functions and closures

* 클로저 MDN정의: 클로저는 독립적인 (자유) 변수를 가리키는 함수이다. 또는, 클로저 안에 정의된 함수는 만들어진 환경을 ‘기억한다’.

* Closures in JavaScript are functions that have access to the parent
scope, even when the parent function has closed.

* Closures are a feature of all functional languages. Traditional imperative languages
do not allow them

var ValueAccumulator = function () {
  
   var values = [];
   var accumulate = function(obj) {
    if (obj) {
      values.push(obj.value);
      return values;
    }
    else {
      return values;
    }
  };
  return accumulate;
};

var accumulator = Valueaccumulator();
accumulator(obj1);
accumulator(obj2);
console.log (accumulator()); // Output: [obj1.value, obj2.value]

## Higher-order functions

*  higher-order function, the array can be worked on by applying that function to each item in
the array to create a new array.

* self invoking function는 higher-order functions의 형태이다 

* higher-order functions는 입력으로 다른 함수를 취하고 출력으로 함수를 리턴한다 

var accumulator2 = ValueAccmulator();

var objects = [obj1, obj2, obj3];

objects.forEach(accumulator2()); // 위와 같은 결과 

## pure functions 

* pure functions 입력으로 넣어진 값으로 계산된 값을 리턴한다. 외부 변수, 전역변수는 사용하지못한다. 그래서 side effect는 걱정없음!

* side effect가 없이 입력이 같으면 언제나 같은 값을 낼 수 있는 함수 

## Anonymous functions 

* 이름없는 함수

## Method chains

console.log([1,2,3,4].reverse().concat([5,6]).map(Math.sqrt));  // 이런식으로 연결

## Recursion

* 함수형프로그래밍 정신과 비슷!

var getLeafs = function(node) {

  if (node.childNodes.length == 0) {
  
    return node.innerText;
    
  }
  else {
  
    return node.childNodes.map(getLeafs);
    
  }
  
}

## Divide and conquer 

## Lazy evaluation 

* also known as non-strict evaluatio

* 값이 필요 할 때까지 계산안함. (텐서플로우같네) 

* lazy.js를 이용해야핢 

// wishful JavaScript pseudocode:
var infinateNums = range(1 to infinity);
var tenPrimes = infinateNums.getPrimeNumbers().first(10);

이러한 경우에 사용 할 수있음

# The functional programmer's toolkit

블라블라

# Setting Up the Functional Programming Environment

## underscore.js 

* 사용 할 이유: jquery랑 비슷해서 익숙하다면 ? 다른 함수들도 많다고함 편의성 

* nderscore's structure may not be ideal or even function!

* 유용하다고 하긴해도 허점이 있는거같아서 한번 써보고 겪어봐야할듯하다 

## fantasy land 

## lazy.js

## bacon.js 

* they're more suited for working with events (onmouseover,
onkeydown, and so on) and reactive properties (scroll position, mouse position,
toggles, and so on).

# Implementing Functional Programming Techniques in JavaScript


## javascript function factories 

function bindFirstArg (func, a) {
  
  return function(b) {
  
    return func(a,b);
    
  };
  
}

var powersOfTwo = bindFirstArg(Math.pow, 2);

console.log(powersOfTwo(3)); // 8

console.log(powersOfTwo(5)); // 32

## partial application

* 미리 인자들중에 특정값을 미리 넣어놓는것 

### partial application from the left

Function.protorype.partialApply = function() {

  var func = this;
  
  args = Arrays.prototype.slice.call(arguments); // partial value
  
  return fuction() {
  
    return func.apply(this, args.concat(
      
      Array.prototype.slice.call(arguments) // 합치는 
      구문
    }};
    
  };
  
};

function num2hex() { 

  function componentToHex(component) {
  
    var hex = component.toString(16);
    
    if (hex.length == 1) {
    
      return "0" + hex;
      
    }
    
    else { 
    
      return hex;
      
    }
    
  }
  
  return Array.prototype.map.call(arguments, componentToHex).join('');
  
}

console.log(nums2hex(100,200)); // '64c8'

console.log(nums2hex(100, 200, 255, 0, 123)); // '64c8ff007b'p

 var muOUI = 123;
 
 var getMacAddress = nums2hex.partitialApply(myOUI); // 맨 왼쪽 인자로 적용된다
 
console.log(getMacAddress()); // '7b'

console.log(getMacAddress(100, 200, 2, 123, 66, 0, 1)); // '7b64c8027b420001'

var shadesOfRed = nums2hex.partialApply(255);

console.log(shadesOfRed(123, 0)); // 'ff7b00'

console.log(shadesOfRed(100, 200)); // 'ff64c8'

 ### partial applicatin from the right 
 
 Function.prototyp.partialApplyRight = function() {
 
  var func = this;
  
  args = Arrays.prototypes.slice.call(arguments); 
  
  return function() { 
    
    return func.apply(
     
      this, [].slice.call(arguments, 0).concat(args); // partial value를 넣는다
      
    };
    
  };
 
var shadesOfBlue = nums2hex.partialApplyRight(255);

console.log(shadesOfBlue(123, 0)); // '7b00ff'

console.log(shadesOfBlue(100, 200)); // '64c8ff'

 ## Currying
 
 * partial applicant와 다른점은 인자를 넣는게 아니라 currying은 다음 인자를 받는 함수를 리턴
 
 * 커링은 상세한 컨트롤이 가능하다 
 
 Function.prototype.curry = function (numArgs) {
 
  var func = this;
  
  numArgs = numArgs || func.length; // 명시적으로 선언이 안되어 있으면 optinally specify
  
  function subCurry (prev) {
  
    return function (arg) {
      
      var args = prev.concat(arg);
      
      if (args.length < numArgs) {
      
        return subCurry(args); // 재귀
        
      }
      
      else { 
      
        return func.apply(this, args);
      
      }
      
    };
    
  }
  
  return subCurry([]);
 
};

function rgb2hex(r, g, b) {
  
  return '#' + nums2hex(r) + nums2hex(g) + nums2hex(b);
  
}

var hexColors = rgb2hex.curry();

console.log(hexColors(11)) // returns a curried function

console.log(hexColors(210)(12)(0))  // returns #d20c00

* 다르게 사용할 수 있는건

var reds = function(g,b){return hexColors(255)(g)(b)};

console.log(reds(11, 12))   // returns #ff0b0c

*** So we have to de ne the number of arguments. ***

* partial application과 currying은 composition에서 큰역할을 한다

## In functional programming, we want everything to be a function. We especially want unary functions if possible. If we can convert all functions to unary functions, then magical things can happen.
함수형 프로그래밍의 정신같다 

* unary functions 오직 한가지 인자만 갖는 함수 polyadic 은 여러가지인자 


## Compose

* 오른쪽부터 실행한다 생각하면 편한듯 함수의 연속 

var roundedSqurt = Math.round.compose(Math.sqrt)

console.log( roundedSqrt(5) ); // Returns 2 

var squaredDate =  roundedSqrt.compose(Date.parse)
   
console.log( squaredDate("January 1, 2014") ); // Returns: 1178370

var compose = function(f, g) {

  return function(x) {
  
    return f(g(x));
    
  };
  
};

Function.prototype.compose = function(prevFunc) {

  vaer nextFunc = this;
  
  return function () {
  
    return nextFunc.call(this, prevFunc.apply(this, arguments));
    
  }
  
* example

function function1(a) {return a + '1';}

function function2(b) {return b + '2';}

function function3(c) return c + '3';}

var composition = function3.compose(function2).compose(function1);

console.log(composition('count')); // returns 'count123'

## sequence - compose in reverse 

* 왼쪽에서 오른쪽으로 가게 하고싶은거 (체인메소드 쓰지그냥)

Function.prototype.sequence = function(prevFunc) {
  
  var nextFunc = this;
  
  return function() {
  
    return prevFunc.call(this, nextFunc.apply(this, arguments));
    
  }
  
}

var sequences = function1.sequence(function2).sequence(function3);

console.log( sequences('count') ); // returns 'count 1 2 3'

## Compositions versus chains

* map을 써서 하는것은 동작하긴 하지만 수학적으로 올바르지 않다 => 의역하기 힘든데 그냥 보기싫은거같다 


## Programming with compose 

* 자주 쓰는 구문

// stringToArray :: string -> [Char]

function stringToArray(s) { return s.split(''); }

//arrayToString :: [char] -> String

function arrayToString(a) { return a.join(''); }

// nextChar :: Char -> Char

function nextChar(c) { return String.fromCharCode(c.charCodeAt(0) + 1) ; }

// previousChar :: Char -> Char

function previousChar(c) { 

  return String.fromCharCode(c.charCodeAt(0) - 1); }
  
// higherColorHex :: Char -> Char

function higherColorHex(c) { 
 
  return c >= 'f' ? 'f' : c == '9' ? 'a' : nextChar(c);}
  
// lowerColorHex :: Char -> Char
function lowerColorHex(c) { 
 
  return c <= '0' ? '0' : c == 'a' ? '9' : previousChar(c); }
  
 // raiseColorHexes :: String -> string 
 
 function raiseColorHexes(arr) { return arr.map(higherColorHex);}
 
 // lowerColorHexes :: String -> String
 
 function lowerColorHexes(arr) { return arr.map(lowerColorHex); }
 
 var lighterColor = arrayToString.compose(raiseColorHexes).compose(stringToArray)
 
 var darkerColor = arrayToString.compose(lowerColorHexes).compose(stringToArray) 
 
console.log( lighterColor('af0189') ); // Returns: 'bf129a'

console.log( darkerColor('af0189')  );  // Returns: '9e0078'

* curry와 compose를 함께

// component2hex :: Ints -> Int

function componentToHex(c) {
  
  var hex = c.toString(16);
  
  return hex.length == 1 ? '0' + hex : hex;
  
}

// nums2hex :: Ints* -> Int

function nums2hex() {

  return Array.prototype.map.call(arguments,
  
  componentToHex
  
  ).join('');
  
}

var lighterColors = lighterColor.compose(nums2hex.curry());

var darkerRed = darkerColor.commpose(nums2hex.partialApply(255)); // 오른쪽에 인자 추가 

Var lighterRgb2hex = ;lighterColor.compose(nums2hex.partialApply());

console.log( lighterColors(123, 0, 22) ); // Returns: 8cff11

console.log( darkerRed(123, 0) ); // Returns: ee6a00

console.log( lighterRgb2hex(123,200,100) ); // Returns: 8cd975


## Category Theory :: 범주이론

## Einstein once said, "If you can't explain it to a 6-year-old, you don't know it yourself".

Morphisms: pure functions, 형태학이라 번역됨

Homomorphic operations : 한개의 카테고리로 제한된다 , 숫자만 곱한다

polymorphic operations : 다양한 카테고리 , 숫자 뿐 아니라 string도 곱한다

1대1 매칭끼리 compose 한다면 이 함수도 1대1매칭 함수이다. 

* js에서 카테고리 이론을 적용하기위해서는 카테고리당 특정한 데이터타입을 사용해야하는데 js는 엄격한 타입시스템이 아니기 때문에 타입체크를 해야한다. 

// 갓 TS

* type이 맞으면 할당하는 함수 정의

var typeOf = function(type) { 

  return function(x) {
  
    if (typeof x === type) {
      
      return x;;
      
    }
    
    else { 
    
      throw new TypeError("Error: "+ type + " expected," + typeof x + "given.");
    }
  
  }
  
}

var str = typeOf('string'),

  num = typeOf('number'),
  
  func = typeOf('function'),
  
  bool = typeOf('boolean'); 
 
