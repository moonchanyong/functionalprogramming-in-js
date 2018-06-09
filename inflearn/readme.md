# inflearn 유인동님 강의

## 1. 함수형 프로그래밍 정의, 순수함수

모든 프로그래밍 패러다임은 성공적인 프로그래밍을 위해 존재한다.

성공적인 프로그래밍은 좋은 프로그램을 만드는일, 좋은프로그램은 사용성, 성능, 확장성, 기획변경에 대한 대응력이 좋다.

이것들을 효율적이고 생산적으로 이루는 일이 성공적인 프로그래밍이다.

* 결론은 프로그래밍 패러다임을 이용하여 사용성, 성능, 확장성, 기획변경에 대한 대응력이 좋은 프로그램을 만들자.

함수형프로그래밍, 사이드이펙트를 줄이고, 조합성을 강조하는 프로그래밍 패러다임

* 부수효과를 줄인다. => 순수함수를 만든다 => 오류를 줄이고 안정성을 높인다.

* 조합성을 강조한다 => 모듈화 수준을 높인다.(잘게 짜른다) => 재사용성을 높여서 생산성을 높인다
```javascript

// 동일한 파라미터에 동일한 결과를 낸다 => 부수효과가 없다.(외부 변수를 변경하지 않는다.)
function add(a, b) {
  return a + b;
}

const c = 10;

// c의값이 변한다면 순수함수라 볼 수 없지만(인자는 같아도 결과가 달라지므로), c가 상수라면 순수함수라 할 수 있다.
function add2(a, b) {
  return a + b + c;
}

let c = 20;

// c의 상태를 변화하므로 부수효과가 있다. => 순수효과가 아니다.(결과는 동일하지만 부수효과를 내므로)
function add3(a, b) {
  c = b;
  return a + b;
}

let obj1 = { val: 10 };

// 들어온 객체의 값을 변경하여 부수효과를 내므로 순수함수가 아니다.
function add4(obj, b) {
  obj.val += b;
}

let obj2 = { val: 20 };

// RORO(recive a object, return object) 패턴, 그리고 순수함수, 값을 변경하지도 않고 새로운 객체를 리턴하므로
function add5(obj, b) {
  return { obj.val + b };
}

```

## 2. 일급함수, add_make, 함수로 함수 실행하기

### 일급함수의 조건
* 변수를 함수에 담을 수 있다.
* 함수를 파리미터로 받을 수 있다.
* 함수를 리턴 할 수 있다.

### add_maker(기본 예제 중 하나)

``` javascript

// 익명함수를 라턴, a를 기억하니까 클로저이다. 이것도 순수 함수이다.
function add_maker(a) {
  return b => a + b;
}

console.log(add_maker(10)(5)); // 15

function f4(f1, f2, f3) {
   return f3(f1() + f2());
}

console.log(f4(() => 2, () => 1, (a) => a * a)); // 9

```
### 순수함수를 만들고 조합하여 함수들의 평가 시점이나 평가방법들을 결정하면서 큰 로직을 만드는게 함수형 프로그래밍


## 3. 요즘 개발 이야기, 함수형 프로그래밍의 정의

### 요즘 개발 이야기

* 재미 / 실시간성: 라이브 방송, 실시간 댓글, 협업, 메신저
* 독창성 / 완성도: 애니메이션, 무한 스크롤, 벽돌(완성도가 높아져야한다.)
* 더 많아져야하는 동시성: 웹 이용률이 증가하여 많은 유저를 처리해야 한다. 비동기 IO, CSP, Actor, STM..
* 더 빨라져야하는 반응성 / 고가용성: ELB, Auto Scaling, OTP Supervisor(서비스가 죽으면 새로 띄우기위해)
* 대용량 / 정확성 / 병렬성: mapReduce, clojure reducers
* 복잡도 / MSA / ...: 많아지고 세밀해지는 도구

### 이러한 부분을 요구해서 FP가 부각된다.
#### 아래의 이유때문에 ..

* 하드웨어 성능이 좋아지고

* 컴파일가 좋아지고

* 함수형프로그래밍 기술

* 좋아지는 분산 / 리액티브 환경

* 동시성 + 병렬성 관련 기술

* 성공적인 적용사례와 영향

### 함수형 프로그래밍의 정의 (마이클포거스 클로저 프로그래밍의 즐거움에서..)
#### 함수형 프로그래밍은 애플리케이션, 함수의 구성요소, 더 나아가 언어 자체를 함수처럼 여기도록 만들고, 이러한 함수 개념을 가장 우선순위에 놓는다.
#### 함수형 사고방식은 문제의 해결방법을 동사(함수)들로 구성(조합)하는 것

#### 함수를 우선순위에 드는것은 무엇인가..

단순히 말하면 함수가 앞에있는것..

* 객체지향은 객체, 데이터부터 만들고 함수를 만들지만 함수형은 함수부터 만들어 데이터를 함수에 맞춘다.

```javascript
// 데이터(객체) 기준
duck.moveLeft();
duck.moveRight();
dog.moveLeft();
dog.moveRight();

// 함수 기준,
moveLeft(dog);
moveRight(duck);
moveLeft({ x: 5. y: 2}); //RORO
moveRight(dog);
```

## 4. 함수형 프로그래밍 하기 회원 목록, map, filter

```javascript
//명령형 코드, 이러한 느낌.. 다 중복이다 반복운은 그래서 중복을 제거해야한다.
  // 1. 30세 이상인 users만 출력한다.
let temp_users = [];
for (let i = 0; i < users.length; i++) {
  if (users[i]).age >= 30) temp_users.push(users[i]);
}
console.log(names)

// 함수형 스타일 filter, map으로 리팩토링, 직접 해당값을 변하지 않고 필터링 된 배열을 return한다.
// 추상화의 단위를 함수로 사용한다. 비교부분을 함수로바꾼다. 응용형 함수래 필터는
function _filter(users, predicate) {
  let new_list = [];
  // 이부분도 forEach를 쓰면 간단해지지만..
  for (let i = 0; i < users.length; i++)
    if (predicate(users[i])) temp_users.push(users[i]);

  return new_list;
}

console.log(_filter(users, (user) => user.age >= 30));
// 함수를 고차로 받거나 함수를 내부에서 실행하는 함수를 고차함수


// map을 만들어보자, 데이터가 어떻게 생겻는지 모른다., 그래서 다형성이좋다, 재사용성이좋다
function _map() {
  let new_list = [];
  for (let i = 0; i < list.length; i+=1) {
    new_list.push(mapper(list[i]));
  }
  return new_list;
}

console.log([], (user) => user.name);
```
