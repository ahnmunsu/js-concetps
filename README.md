# Javascript 개념 정리
https://github.com/leonardomso/33-js-concepts을 참고하여 자바 스크립트 개발자가 알아야할 개념을 정리했다.

---

## 목차
1.  **[Call Stack](#call-stack)**
1.  **[Primitive Types](#primitive-types)**
1.  **[Value Types and Reference Types](#value-types-and-reference-types)**
1.  **[Implicit, Explicit, Nominal, Structuring and Duck Typing](#implicit-explicit-nominal-structuring-and-duck-typing)**
1.  **[== vs === vs typeof](#-vs--vs-typeof)**
1.  **[Function Scope, Block Scope and Lexical Scope](#function-scope-block-scope-and-lexical-scope)**
1.  **[Expression vs Statement](#expression-vs-statement)**
1.  **[IIFE, Modules and Namespaces](#iife-modules-and-namespaces)**
1.  **[Message Queue and Event Loop](#message-queue-and-event-loop)**
1.  **[setTimeout, setInterval and requestAnimationFrame](#settimeout-setinterval-and-requestanimationframe)**
1.  **[JavaScript Engines](#javascript-engines)**
1.  **[Bitwise Operators, Type Arrays and Array Buffers](#bitwise-operators-type-arrays-and-array-buffers)**
1.  **[DOM and Layout Trees](#dom-and-layout-trees)**
1.  **[Factories and Classes](#factories-and-classes)**
1.  **[this, call, apply and bind](#this-call-apply-and-bind)**
1.  **[new, Constructor, instanceof and Instances](#new-constructor-instanceof-and-instances)**
1.  **[Prototype Inheritance and Prototype Chain](#prototype-inheritance-and-prototype-chain)**
1.  **[Object.create and Object.assign](#objectcreate-and-objectassign)**
1.  **[map, reduce, filter](#map-reduce-filter)**
1.  **[Pure Functions, Side Effects and State Mutation](#pure-functions-side-effects-and-state-mutation)**
1.  **[Closures](#closures)**
1.  **[High Order Functions](#high-order-functions)**
1.  **[Recursion](#recursion)**
1.  **[Collections and Generators](#collections-and-generators)**
1.  **[Promises](#promises)**
1.  **[async/await](#asyncawait)**
1.  **[Data Structures](#data-structures)**
1.  **[Expensive Operation and Big O Notation](#expensive-operation-and-big-o-notation)**
1.  **[Algorithms](#algorithms)**
1.  **[Inheritance, Polymorphism and Code Reuse](#inheritance-polymorphism-and-code-reuse)**
1.  **[Design Patterns](#design-patterns)**
1.  **[Partial Applications, Currying, Compose and Pipe](#partial-applications-currying-compose-and-pipe)**
1.  **[Clean Code](#clean-code)**

---

## Call Stack
...
**[⬆ 목차](#목차)**

---

## Primitive Types
*  Number
*  String
*  Boolean
*  Null
*  Undefined
*  Ojbect
### Number
#### 정수
```
var decimalNum = 100; // 기본 숫자 리터럴 형식 10진수로 초기화
var octalNum = 010; // 8진수로 초기화
var hexNum = 0x10; // 16진수로 초기화
```
#### 부동소수점
```
var floatNum1 = 3.14;
var floatNum2 = 3.125e7;
```
##### 부동소수점 사칙연산 부정확
0.1 + 0.2 결과는 0.30000000000000004로 아래 코드는 의도대로 동작하지 않는다.
```
var f1 = 0.1;
var f2 = 0.2;

if (f1 + f2 == 0.3) {
    do_something();
}
```
#### 숫자 범위
*  최소값 : Number.MIN_VALUE (5e-324)
*  최대값 : Number.MAX_VALUE (1.7976931348623157e+308)
*  최소, 최대를 벗어나면 양수는 Infinity, 음수는 -Infinity로 변환된다.
#### NaN
*  Not-a-Number의 줄임말
*  값이 숫자가 아님을 뜻한다.
*  숫자를 0으로 나눈 경우 결과 값이 NaN이다.
*  NaN == NaN은 false이다.
*  isNaN 함수를 사용하여 검사한다.
#### 문자열을 숫자로 변환하는 함수
*  Number()
*  parseInt()
*  parseFloat()

---

### String
*  텍스트 데이터를 나타내는데 사용한다.
*  16비트 부호없는 정수 값 요소들의 집합이다.
*  String 의 길이는 String이 가지고 있는 요소의 갯수이다.
*  문자열이 생성되면, 그 문자열을 수정할 수 없다.
*  기존 문자열을 String.substr(), String.concat() 같은 method나 접합 연산자(+)를 사용해 새로운 문자열을 만든다.
#### 문자열로 변환하는 함수
*  toString() method는 값에 해당하는 문자열을 반환한다.
```
var hundred = 100;
var hundred_string = hundred.toString(); // 문자열 "100"
var is_true = true;
var is_true_string = is_true.toString(); // 문자열 "true"
var hex_num = 10;
var hex_num_string = hex_num.toString(16); // 16진수 문자열 "a"
```
*  String() 함수는 null이나 undefined도 사용 가능하다. (*toString은 불가능*)
```
var im_null = null;
var im_null_string = String(im_null); // 문자열 "null"
var im_undefined = undefined;
var im_undefined_string = String(im_undefeind); // 문자열 "undefined"
```

### Boolean
주어진 조건이 참인지 거짓인지 나타내는 자료형이다.
```
1 < 2; // true
1 > 2; // false
3 === 3; // true
3 !== 3; // false
Number.isFinite(Infinity); // false
Number.isNaN(NaN); // true
'hello'.includes('ll'); // true
```

### Null
*  어떤 값이 *의도적으로* 비어있음을 표현한다.
*  null 값을 가진 객체 변수는 어떠한 객체도 가리키고 있지 않는 상태이다.
*  함수에서 리턴값을 기대하지만 일치하는 값이 없을 경우에 null을 리턴하는 식으로 사용한다.
*  null과 undefined 차이
```
typeof null          // "object" (하위호환 유지를 위해 "null"이 아님)
typeof undefined     // "undefined"
null === undefined   // false
null  == undefined   // true
null === null        // true
null == null         // true
!null                // true
isNaN(1 + null)      // false
isNaN(1 + undefined) // true
```

### Undefined
*  선언한 후 값을 할당하지 않은 변수 혹은 값이 주어지지 않은 인수에 자동으로 할당된다.
```
var x; // 값을 할당하지 않고 변수 선언
console.log("x's value is", x) // "x's value is undefined" 출력
```

### Symbol
*  ECMAScript 2015에서 새로 등장한 원시 타입이다.
*  전역 function/object인 Symbol을 호출하면 타입이 symbol이 된다.
```
var mySymbol = Symbol(); // typeof mySymbol -> "symbol"
```
*  Symbol은 “new” 키워드를 사용하지 못 한다.
```
var mySymbol = new Symbol(); //throws error
```
*  Symbol은 description을 가진다.
```
// mySymbol variable now holds a "symbol" unique value
// its description is "some text"
var mySymbol = Symbol('some text');
```
*  Symbol은 unique하다.
```
var mySymbol1 = Symbol('some text');
var mySymbol2 = Symbol('some text');
mySymbol1 == mySymbol2 // false
```
*  Symbol.for를 사용하면 Symbol이 싱글톤처럼 작동한다.
```
var mySymbol1 = Symbol.for('some key'); //creates a new symbol
var mySymbol2 = Symbol.for('some key'); // **returns the same symbol
mySymbol1 == mySymbol2 //true
```
*for 메서드를 사용하는 이유는 어떤 한곳에서 Symbol을 만들고 다른 곳에서 같은 Symbol에 접근하기 위해서이다.*
*  Symbol은 객체 프로퍼티 키일 수 있다.
객체에 Symbol을 속성키로 붙일 수 있다. Symbol은 unique 하기 때문에 이름 충돌없이 객체의 속성을 계속 추가할 수 있다.
```
var mySymbol = Symbol("some car description");
var myObject = { name: 'bmw' };
myObject[mySymbol] = 'This is a car';
console.log(mySymbol); // Symbol(some car description)
console.log(myObject[mySymbol]); // This is a car
console.log(myObject.mySymbol); // x
```
**[⬆ 목차](#목차)**

---

## Value Types and Reference Types
...
**[⬆ 목차](#목차)**

---

## Implicit, Explicit, Nominal, Structuring and Duck Typing
### Type Coersion
```
true + false
==> 1 + 0
==> 1

`+` 연산자가 true와 false를 numeric conversion한다.  
```
```
12 / '6'
==> 12 / 6
==> 2

`/` 연산자가 string '6'을 numeric conversion한다.
```
```
"number" + 15 + 3 
==> "number15" + 3 
==> "number153"

`+` 연산자는 좌에서 우로 결합한다. 그래서 "number"와 15가 먼저 실행되는데 `+` 연산자가 숫자 15를 string conversion한다.  
그 결과 "number15"가 되고 다시 숫자 3이 string conversion된다.
```
```
15 + 3 + "number" 
==> 18 + "number" 
==> "18number"

15 + 3이 18로 계산되고 `+` 연산자가 18을 string conversion한다.
```
```
[1] > null
==> '1' > 0
==> 1 > 0
==> true

`>` 연산자가 [1]과 null을 numeric conversion을 한다.
```
```
"foo" + + "bar" 
==> "foo" + (+"bar") 
==> "foo" + NaN 
==> "fooNaN"

단항 연산자 `+` 연산자가 결합 순위가 높기 때문에 +"bar"이 먼저 평가된다.  
그리고 이항 `+` 연산자가 NaN을 string conversion한다.
```
```
'true' == true
==> NaN == 1
==> false

false == 'false'   
==> 0 == NaN
==> false

`==` 연산자는 numeric conversion를 한다. 'true'는 NaN으로, true는 1로 변환된다.
```
```
null == ''
==> false

`==` 연산자는 보통 numeric conversion을 하지만, null과 함께 할 때만 그렇지 않다.  
null은 null이나 undefined일 때만 같고 다른 모든 것들과는 다르다.
```
```
!!"false" == !!"true"  
==> true == true
==> true

`!!` 연산자는 'true'와 'false' 문자열이 둘 다 빈 문자열이 아니기 때문에 true로 변환한다.  
```
```
['x'] == 'x'  
==> 'x' == 'x'
==>  true

`==` 연산자는 Array에 대해 numeric conversion을 한다. Array의 `valueOf()` method는 Array 자신을 리턴하는데 그것은 원시값(primitive)이 아니기 때문에 무시된다.  
Array의 `toString()`은 ['x']를 'x' 문자열로 변환한다.
```
```
[] + null + 1  
==>  '' + null + 1  
==>  'null' + 1  
==> 'null1'

`+` 연산자는 []을 numeric conversion한다. Array의 `valueOf()` method는 그 자신을 리턴하기 때문에 무시된다.  
Array의 `toString()`은 빈 문자열을 리턴한다.
```
```
0 || "0" && {}  
==>  (0 || "0") && {}
==> (false || true) && true  // internally
==> "0" && {}
==> true && true             // internally
==> {}

논리 `||`, `&&` 연산자는 피연산자를 내부적으로 boolean으로 변환한다. 하지만 리턴은 boolean이 아닌 원래 피연산자를 리턴한다.  
```
```
[1,2,3] == [1,2,3]
==>  false

피연산자들이 같은 타입이기 때문에 형변환이 필요없다. 그래서 `==` 연산자는 동일한 object인지 확인한다. (object의 내용이 같은지 확인하는 것이 아니다.)  
이 두 Array는 각각의 다른 인스턴스이기 때문에 같지 않다. 
```
```
{}+[]+{}+[1]
==> +[]+{}+[1]
==> 0 + {} + [1]
==> 0 + '[object Object]' + [1]
==> '0[object Object]' + [1]
==> '0[object Object]' + '1'
==> '0[object Object]1'

모든 피연산자가 원시값이 아니다.  그래서 `+` 연산자는 왼쪽부터 numeric conversion을 한다.  
첫 번째 {}는 object 리터럴이 아닌 블록문으로 처리되어 무시된다. 그래서 +[] 표현부터 평가되는데 `toString()` method에 의해 빈 문자열로 변환되고 그 다음 0으로 된다.
```
```
!+[]+[]+![]  
==> (!+[]) + [] + (![])
==> !0 + [] + false
==> true + [] + false
==> true + '' + false
==> 'truefalse'

연산자 우선 순위를 따라 처리된다.
```
```
new Date(0) - 0
==> 0 - 0
==> 0

`-` 연산자는 Date를 numeric conversion한다. `Date.valueOf()`는 Unix epoch부터 밀리초를 리턴한다.
```
```
new Date(0) + 0
==> 'Thu Jan 01 1970 02:00:00 GMT+0200 (EET)' + 0
==> 'Thu Jan 01 1970 02:00:00 GMT+0200 (EET)0'

`+` 연산자는 default conversion을 한다. Date는 string conversion이 default라서 `toString()` method가 사용된다.
```

### Nonimal Typing
C++, Java, Swift 같은 언어들이 주요 nominal type system이다.
```
class Foo { method(input: string) { /* ... */ } }
class Bar { method(input: string) { /* ... */ } }

let foo: Foo = new Bar(); // Error!
```
클래스 이름이 다른 변수에 대입하려고 할 때 에러가 발생한다.

### Structural Typing
OCaml, Haskell, Elm 같은 언어들이 주요 structural type system이다.
```
class Foo { method(input: string) { /* ... */ } }
class Bar { method(input: string) { /* ... */ } }

let foo: Foo = new Bar(); // Works!
```
structure가 완벽하게 같은 클래스는 이름이 달라도 대입이 가능하다.  
그러나 클래스 내용을 변경하면 에러가 발생한다.  
```
class Foo { method(input: string) { /* ... */ } }
class Bar { method(input: number) { /* ... */ } }

let foo: Foo = new Bar(); // Error!
```

### Duck Typing
*  Duck Typing은 인자가 어떤 형인지 상관 없이 그 동작을 할 수 있는지를 확인하여 객체를 판단하는 방법이다. 
*  "오리처럼 걷고, 오리처럼 소리 내면 오리로 간주한다(If it walks like a duck and quacks like a duck, I would call it a duck.)"는 말에서 유래했다.
아래는 자동 급식 장치를 Javascript로 구현한 예제이다. 자동 급식 장치 앞에서 "꽥" 소리를 내면, 즉 quack() method를 수행하면 모이를 제공한다.
```
function FeedDispenser() {}; 
FeedDispenser.prototype.requestFeed = function(quackable) {
    return (quackable.quack() != null) ? new Feed() : null; 
};
```

다음은 Goose 객체를 구현한 예제이다.
```
function Goose() {};
Goose.prototype.honk = function() {
    return honk();
}
```

프로토타입 객체에 quack() 메서드를 추가로 구현한다.
```
Goose.prototype.quack = function() {
    return this.honk(); 
}
```

위와 같이 확장된 Goose 인스턴스를 자동 급식 장치에 적용하면 다음과 같다.
```
var goose = new Goose();
var feedDispenser = new FeedDispenser();
var feed = feedDispenser.requestFeed(goose);
console.log(feed != null); // true
```
**[⬆ 목차](#목차)**

---

## == vs === vs typeof
...
**[⬆ 목차](#목차)**

---

## Function Scope, Block Scope and Lexical Scope
...
**[⬆ 목차](#목차)**

---

## Expression vs Statement
...
**[⬆ 목차](#목차)**

---

## IIFE, Modules and Namespaces
...
**[⬆ 목차](#목차)**

---

## Message Queue and Event Loop
...
**[⬆ 목차](#목차)**

---

## setTimeout, setInterval and requestAnimationFrame
...
**[⬆ 목차](#목차)**

---

## JavaScript Engines
...
**[⬆ 목차](#목차)**

---

## Bitwise Operators, Type Arrays and Array Buffers
...
**[⬆ 목차](#목차)**

---

## DOM and Layout Trees
...
**[⬆ 목차](#목차)**

---

## Factories and Classes
...
**[⬆ 목차](#목차)**

---

## this, call, apply and bind
...
**[⬆ 목차](#목차)**

---

## new, Constructor, instanceof and Instances
...
**[⬆ 목차](#목차)**

---

## Prototype Inheritance and Prototype Chain
...
**[⬆ 목차](#목차)**

---

## Object.create and Object.assign
...
**[⬆ 목차](#목차)**

---

## map, reduce, filter
...
**[⬆ 목차](#목차)**

---

## Pure Functions, Side Effects and State Mutation
...
**[⬆ 목차](#목차)**

---

## Closures
...
**[⬆ 목차](#목차)**

---

## High Order Functions
...
**[⬆ 목차](#목차)**

---

## Recursion
...
**[⬆ 목차](#목차)**

---

## Collections and Generators
...
**[⬆ 목차](#목차)**

---

## Promises
...
**[⬆ 목차](#목차)**

---

## async/await
...
**[⬆ 목차](#목차)**

---

## Data Structures
...
**[⬆ 목차](#목차)**

---

## Expensive Operation and Big O Notation
...
**[⬆ 목차](#목차)**

---

## Algorithms
...
**[⬆ 목차](#목차)**

---

## Inheritance, Polymorphism and Code Reuse
...
**[⬆ 목차](#목차)**

---

## Design Patterns
...
**[⬆ 목차](#목차)**

---

## Partial Applications, Currying, Compose and Pipe
...
**[⬆ 목차](#목차)**

---

## Clean Code
...
**[⬆ 목차](#목차)**

---
