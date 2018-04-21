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
