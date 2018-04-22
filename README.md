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
