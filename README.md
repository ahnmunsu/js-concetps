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
*  Symbol
### Number
#### 정수
```javascript
var decimalNum = 100; // 기본 숫자 리터럴 형식 10진수로 초기화
var octalNum = 010; // 8진수로 초기화
var hexNum = 0x10; // 16진수로 초기화
```
#### 부동소수점
```javascript
var floatNum1 = 3.14;
var floatNum2 = 3.125e7;
```
##### 부동소수점 사칙연산 부정확
0.1 + 0.2 결과는 0.30000000000000004로 아래 코드는 의도대로 동작하지 않는다.
```javascript
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
```javascript
var hundred = 100;
var hundred_string = hundred.toString(); // 문자열 "100"
var is_true = true;
var is_true_string = is_true.toString(); // 문자열 "true"
var hex_num = 10;
var hex_num_string = hex_num.toString(16); // 16진수 문자열 "a"
```
*  String() 함수는 null이나 undefined도 사용 가능하다. (*toString은 불가능*)
```javascript
var im_null = null;
var im_null_string = String(im_null); // 문자열 "null"
var im_undefined = undefined;
var im_undefined_string = String(im_undefeind); // 문자열 "undefined"
```

---

### Boolean
주어진 조건이 참인지 거짓인지 나타내는 자료형이다.
```javascript
1 < 2; // true
1 > 2; // false
3 === 3; // true
3 !== 3; // false
Number.isFinite(Infinity); // false
Number.isNaN(NaN); // true
'hello'.includes('ll'); // true
```

---

### Null
*  어떤 값이 *의도적으로* 비어있음을 표현한다.
*  null 값을 가진 객체 변수는 어떠한 객체도 가리키고 있지 않는 상태이다.
*  함수에서 리턴값을 기대하지만 일치하는 값이 없을 경우에 null을 리턴하는 식으로 사용한다.
*  null과 undefined 차이
```javascript
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

---

### Undefined
*  선언한 후 값을 할당하지 않은 변수 혹은 값이 주어지지 않은 인수에 자동으로 할당된다.
```javascript
var x; // 값을 할당하지 않고 변수 선언
console.log("x's value is", x) // "x's value is undefined" 출력
```

---

### Symbol
*  ECMAScript 2015에서 새로 등장한 원시 타입이다.
*  전역 function/object인 Symbol을 호출하면 타입이 symbol이 된다.
```javascript
var mySymbol = Symbol(); // typeof mySymbol -> "symbol"
```
*  Symbol은 “new” 키워드를 사용하지 못 한다.
```javascript
var mySymbol = new Symbol(); //throws error
```
*  Symbol은 description을 가진다.
```javascript
// mySymbol variable now holds a "symbol" unique value
// its description is "some text"
var mySymbol = Symbol('some text');
```
*  Symbol은 unique하다.
```javascript
var mySymbol1 = Symbol('some text');
var mySymbol2 = Symbol('some text');
mySymbol1 == mySymbol2 // false
```
*  Symbol.for를 사용하면 Symbol이 싱글톤처럼 작동한다.
```javascript
var mySymbol1 = Symbol.for('some key'); //creates a new symbol
var mySymbol2 = Symbol.for('some key'); // **returns the same symbol
mySymbol1 == mySymbol2 //true
```
*for 메서드를 사용하는 이유는 어떤 한곳에서 Symbol을 만들고 다른 곳에서 같은 Symbol에 접근하기 위해서이다.*
*  Symbol은 객체 프로퍼티 키일 수 있다.
객체에 Symbol을 속성키로 붙일 수 있다. Symbol은 unique 하기 때문에 이름 충돌없이 객체의 속성을 계속 추가할 수 있다.
```javascript
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

`+` 연산자는 좌에서 우로 결합한다. 
그래서 "number"와 15가 먼저 실행되는데 `+` 연산자가 숫자 15를 string conversion한다.  
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

`==` 연산자는 Array에 대해 numeric conversion을 한다. 
Array의 `valueOf()` method는 Array 자신을 리턴하는데 그것은 원시값(primitive)이 아니기 때문에 무시된다.  
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

논리 `||`, `&&` 연산자는 피연산자를 내부적으로 boolean으로 변환한다. 
하지만 리턴은 boolean이 아닌 원래 피연산자를 리턴한다.  
```
```
[1,2,3] == [1,2,3]
==>  false

피연산자들이 같은 타입이기 때문에 형변환이 필요없다. 
그래서 `==` 연산자는 동일한 object인지 확인한다. (object의 내용이 같은지 확인하는 것이 아니다.)  
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
첫 번째 {}는 object 리터럴이 아닌 블록문으로 처리되어 무시된다. 
그래서 +[] 표현부터 평가되는데 `toString()` method에 의해 빈 문자열로 변환되고 그 다음 0으로 된다.
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

---

### Nonimal Typing
C++, Java, Swift 같은 언어들이 주요 nominal type system이다.
```javascript
class Foo { method(input: string) { /* ... */ } }
class Bar { method(input: string) { /* ... */ } }

let foo: Foo = new Bar(); // Error!
```
클래스 이름이 다른 변수에 대입하려고 할 때 에러가 발생한다.

---

### Structural Typing
OCaml, Haskell, Elm 같은 언어들이 주요 structural type system이다.
```javascript
class Foo { method(input: string) { /* ... */ } }
class Bar { method(input: string) { /* ... */ } }

let foo: Foo = new Bar(); // Works!
```
structure가 완벽하게 같은 클래스는 이름이 달라도 대입이 가능하다.  
그러나 클래스 내용을 변경하면 에러가 발생한다.  
```javascript
class Foo { method(input: string) { /* ... */ } }
class Bar { method(input: number) { /* ... */ } }

let foo: Foo = new Bar(); // Error!
```

---

### Duck Typing
*  Duck Typing은 인자가 어떤 형인지 상관 없이 그 동작을 할 수 있는지를 확인하여 객체를 판단하는 방법이다. 
*  "오리처럼 걷고, 오리처럼 소리 내면 오리로 간주한다(If it walks like a duck and quacks like a duck, I would call it a duck.)"는 말에서 유래했다.
아래는 자동 급식 장치를 Javascript로 구현한 예제이다. 자동 급식 장치 앞에서 "꽥" 소리를 내면, 즉 quack() method를 수행하면 모이를 제공한다.
```javascript
function FeedDispenser() {}; 
FeedDispenser.prototype.requestFeed = function(quackable) {
    return (quackable.quack() != null) ? new Feed() : null; 
};
```

다음은 Goose 객체를 구현한 예제이다.
```javascript
function Goose() {};
Goose.prototype.honk = function() {
    return honk();
}
```

프로토타입 객체에 quack() 메서드를 추가로 구현한다.
```javascript
Goose.prototype.quack = function() {
    return this.honk(); 
}
```

위와 같이 확장된 Goose 인스턴스를 자동 급식 장치에 적용하면 다음과 같다.
```javascript
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
###  Global Scope  
Javascript document에는 오직 하나의 global scope만 존재한다.  
함수 바깥에 정의된 변수는 global scope에 속한다.
```javascript
// the scope is by default global
var name = 'msahn';
```
```javascript
var name = 'msahn';

console.log(name); // logs 'msahn'

function logName() {
    console.log(name); // 'name' is accessible here and everywhere else
}

logName(); // logs 'msahn'
```

---

### Local Scope  
함수 안에서 정의된 변수는 local scope에 속한다.
```javascript
// Global Scope
function someFunction() {
    // Local Scope #1
    function someOtherFunction() {
        // Local Scope #2
    }
}

// Global Scope
function anotherFunction() {
    // Local Scope #3
}
// Global Scope
```

---

### Block statements
Block statement는 function과 달리 `if`와 `switch` 같은 condition문이나 `for`와 `while`같은 loop문이다.
```javascript
if (true) {
    // this 'if' conditional block doesn't create a new scope
    var name = 'msahn'; // name is still in the global scope
}

console.log(name); // logs 'msahn'
```
```javascript
if (true) {
    // this 'if' conditional block doesn't create a scope

    // name is in the global scope because of the 'var' keyword
    var name = 'msahn';
    // likes is in the local scope because of the 'let' keyword
    let likes = 'Coding';
    // skills is in the local scope because of the 'const' keyword
    const skills = 'JavaScript';
}

console.log(name); // logs 'msahn'
console.log(likes); // Uncaught ReferenceError: likes is not defined
console.log(skills); // Uncaught ReferenceError: skills is not defined
```

---

### Lexical Scope  
lexical scope는 포개어진 함수 그룹을 의미한다.  
안쪽의 함수는 그 부모 scope의 변수와 resource에 접근이 가능하다.
```javascript
function grandfather() {
    var name = 'msahn';
    // likes is not accessible here
    function parent() {
        // name is accessible here
        // likes is not accessible here
        function child() {
            // Innermost level of the scope chain
            // name is also accessible here
            var likes = 'Coding';
        }
    }
}
```

**[⬆ 목차](#목차)**

---

## Expression vs Statement
...
**[⬆ 목차](#목차)**

---

## IIFE, Modules and Namespaces
### IIFE (Immediately-Invoked Function Expressions)
*  IIFE는 정의와 동시에 호출되는 함수이다.
```javascript
(function sayHi() {
        alert('Hi there!'); 
    }
)(); 
// alerts 'Hi there!'
```
*  IIFE로 인자 전달하기
```javascript
(function (name) { 
        alert(`Hi, ${name}`); 
    }
)('Kim'); 
// alerts 'Hi, Kim'
```
*  IIFE의 주요 사용 용도는 private scope를 만들기 위해서 이다. 다시 말해 내부의 코드가 global scope를 더럽히는 것을 방지하고 내부 변수를 외부에서 참조하지 못 하도록 보호하기 위해서 이다.  
아래는 버튼 클릭 수를 세는 예제이다.
```html
<!-- button.html --> 
<html>
    <body>
        <button id='button'>Click me!</button>
        <script src='button.js'>
        </script> 
    </body>
</html>
```
```javascript
// button.js
const button = document.getElementById('button');

button.addEventListener('click', (function() {
    let count = 0;
    return function() {
        count += 1;

        if (count === 2) {
            alert('This alert appears every other press!');
            count = 0;
        }
    };
})());
```
*  특정한 실행 context를 생성하기 위해 오직 한 번 실행되는 의도로 사용된다.
*  ES5에서는 변수의 scope가 function에 의해서만 정해질 수 있었기 때문에 사용 되었다. ES6부터는 let, const, module로 대체할 수 있다.

---

### Modules
*  클라이언트 사이드 자바스크립트는 script 태그를 사용하여 외부의 스크립트 파일을 가져올 수는 있지만, 파일마다 독립적인 파일 스코프를 갖지 않고 하나의 전역 객체(Global Object)를 공유한다.
*  서버 사이드 자바스크립트 런타임 환경인 Node.js는 모듈 시스템의 사실상 표준(de facto standard)인 CommonJS를 채택하였고 독자적인 진화를 거쳐 현재는 CommonJS 사양과 100% 동일하지는 않지만 기본적으로 CommonJS 방식을 따르고 있다.
*  ES6에서는 클라이언트 사이드 자바스크립트에서도 동작하는 모듈 기능을 추가하였다. 2019년 11월 현재, 모던 브라우저(Chrome 61, FF 60, SF 10.1, Edge 16 이상)에서 ES6 모듈을 사용할 수 있다.
*  script 태그에 type="module" 어트리뷰트를 추가하면 로드된 자바스크립트 파일은 모듈로서 동작한다. ES6 모듈의 파일 확장자는 모듈임을 명확히 하기 위해 mjs를 사용하도록 권장한다.
```html
<script type="module" src="lib.mjs"></script>
<script type="module" src="app.mjs"></script> 
```
*  단, 아래와 같은 이유로 아직까지는 브라우저가 지원하는 ES6 모듈 기능보다는 Webpack 등의 모듈 번들러를 사용하는 것이 일반적이다.
    *  IE를 포함한 구형 브라우저는 ES6 모듈을 지원하지 않는다.
    *  브라우저의 ES6 모듈 기능을 사용하더라도 트랜스파일링이나 번들링이 필요하다.
    *  아직 지원하지 않는 기능(Bare import 등)이 있다.
    *  점차 해결되고는 있지만 아직 몇가지 이슈가 있다.

---

### Namespaces
*  Namespace 패턴은 전역 공간에 변수를 생성하고 코드를 사용하는 것을 방지하기 위해 네임스페이스라는 분리된 공간을 만들어 그 안에서 변수를 선언하고 코드를 작성하도록 하는 패턴이다.
*  Namespace 생성
```javascript
var NAMESPACE = {}; // 네임스페이스 생성

NAMESPACE.number = 1; // 변수 생성
NAMESPACE.func = function() {}; // 함수 생성
NAMESPACE.obj = {}; // 객체 생성
``` 
*  Namespace 이름은 충돌 방지를 위해 모두 대문자를 사용한다.
*  모든 변수와 함수에 접두어를 붙여야 하기 때문에 전체적으로 코드량이 약간 더 많아지고 따라서 파일 크기도 늘어난다.
*  이름이 중첩되고 길어지므로 프로퍼티를 판별하기 위한 검색 작업도 길고 느려진다. 

**[⬆ 목차](#목차)**

---

## Message Queue and Event Loop
...
**[⬆ 목차](#목차)**

---

## setTimeout, setInterval and requestAnimationFrame
### setTimeout
*  setTimeout 함수는 설정한 시간만큼 기다린 후 단 한번 지정한 함수를 실행한다.
*  정지하려면 clearTimeout을 호출한다.
```javascript
/* 실행 */
var loopTimer = setTimeout(function(){ /* process... */}, delay);
/* 정지 */
clearTimeout(loopTimer);
```
*  setTimeout 함수는 단 한번 지정된 함수를 실행하지만 재귀 호출을 통해 반복적으로 실행 할 수 있다.
*  만약 delay를 100ms로 설정했다면 지정된 함수가 실행되는 간격은 100ms 이상이다.
![settimeout](./img/settimeout.PNG)

### setInterval
*  setInterval 함수는 설정한 시간만큼 기다린 후 지정한 함수를 실행하고 이 동작을 반복한다.
*  정지하려면 clearInterval을 호출한다.
```javascript
/* 실행 */
var onceTimer = setInterval(function(){ /* process... */ }, delay); 
/* 정지 */
clearInterval(onceTimer);
```
*  브라우저가 함수를 실행할 수 없는 상태(busy)라면 이벤트를 최대 길이가 1인 큐에 저장한다.
*  큐에 이미 이벤트가 존재한다면 그 이벤트는 skip 된다.
*  만약 delay를 100ms로 설정했다면 실제 delay는 100ms보다 적다.
![setinterval](./img/setinterval.PNG)

### setTimeout, setInterval limitations
*  브라우저는 setTimeout의 5개 이상의 중첩 호출 또는 setInterval(5 번째 호출 이후)에 대한 최소 지연을 4ms로 제한한다. (historical reason?)
*  브라우저 내장 타이머는 여러 이유들로 인해 느려질 수 있다.
    *  CPU 과부하
    *  브러우저 탭이 백그라운드 모드에 있을 때
    *  랩탑이 배터리로 사용 중 일 때

### requestAnimationFrame
*  전통적으로 javascript에서 애니메이션을 만들 때는 setTimeout이나 setInterval을 사용했었다.
```js
var adiv = document.getElementById('mydiv')
var leftpos = 0
setInterval(function(){
    leftpos += 5
    adiv.style.left = leftpos + 'px' // move div by 5 pixels each time
}, 50) // run code every 50 milliseconds
```
*  위 코드는 논리적으로 그럴듯 하지만 실제 동작은 완벽하지 않다. 이유는 다음과 같다.
    *  시스템 리소스 변동으로 인해 지연 간격이 일정하지 않다.
    *  화면을 지속적으로 변경하기 위해 과도하게 setTimeout, setInterval을 사용하면 layout thrashing으로 인해 성능 저하가 유발된다.
*  requestAnimationFrame method는 실제 화면이 갱신되어 표시되는 주기에 따라 함수를 호출해주기 때문에 자바스크립트가 프레임 시작 시 실행되도록 보장한다.
*  보통 1초에 60회 정도 실행이 되지만 대부분의 브라우저는 W3C 권장사항에 따라 디스플레이 주사율과 일치하도록 실행된다.
*  requestAnimationFrame()는 현재 창에 표시 되지 않으면 애니메이션을 중지한다.
```js
var adiv = document.getElementById('mydiv')
var leftpos = 0
requestAnimationFrame(function(timestamp){
    leftpos += 5
    adiv.style.left = leftpos + 'px'
})
```
**[⬆ 목차](#목차)**

---

## JavaScript Engines
...
**[⬆ 목차](#목차)**

---

## Bitwise Operators, Type Arrays and Array Buffers
### Bitwise Operators
연산자 | 사용법 | 설명
---|---|--
Bitwise AND|a & b|왼쪽과 오른쪽 피연사자의 비트가 1이면 각 비트를 1로 리턴
Bitwise OR|a | b|왼쪽이나 오른쪽 피연산자의 비트가 1이면 각 비트를 1로 리턴
Bitwise XOR|a ^ b|왼쪽이나 오른쪽 피연산자의 비트 중 한 쪽만 1이면 각 비트를 1로 리턴
Bitwise NOT|~ a|피연산자의 모든 비트를 반전 시킴
Left shift|a << b|a를 오른쪽에서 왼쪽으로 b 비트 만큼 이동 시키고 0으로 채움
Sign-propagating right shift|a >> b|a를 왼쪽에서 오른쪽으로 b 비트 만큼 이동 시키고 양수일 경우 0으로, 음수일 경우 1로 채움
Zero-fill right shift|a >>> b|a를 왼쪽에서 오른쪽으로 b 비트 만큼 이동 시키고 0으로 채움
  
### Type Arrays and Array Buffers
*  원시(raw) 이진 데이터 엑세스를 위한 객체
*  버퍼와 뷰로 나뉘어 짐
*  버퍼(ArrayBuffer 객체에 의해 구현됨)는 데이터 부분(chunk, 덩어리)을 나타내는 객체
*  형식화 배열 뷰

이름 | 범위 | 설명 | 타입
---|---|---|---
Int8Array|-128 ~ 127|부호있는 8비트 정수|char
Uint8Array|0 ~ 255|부호없는 8비트 정수|unsigned char
Int16Array|-32,768 ~ 32,767|부호있는 16비트 정수|short
Uint16Array|0 ~ 65,535|부호없는 16비트 정수|unsigned short
Int32Array|-2,147,483,648 ~ 2,147,483,647|부호있는 32비트 정수|int
Uint32Array|0 ~ 4,294,967,295|부호없는 32비트 정수|unsigned int
Float32Array|-3.4 x 10의 38승 ~ 3.4 x 10의 38승|32-bit IEEE floating point number|float
Float64Array|-1.79 x 10의 308승 ~ 1.79 x 10의 308승|64-bit IEEE floating point number|double

![typed_arrays](./img/typed_arrays.png)

*  뷰는 버퍼에 데이터를 읽거나 쓸 수 있는 getter/setter API를 제공하는 저레벨 인터페이스
*  버퍼 사용
```js
var buffer = new ArrayBuffer(16);

if (buffer.byteLength === 16) {
  console.log("Yes, it's 16 bytes.");
} else {
  console.log("Oh no, it's the wrong size!");
}
```
*  뷰 사용
```js
var buffer = new ArrayBuffer(16);

var int32View = new Int32Array(buffer);

for (var i = 0; i < int32View.length; i++) {
  int32View[i] = i * 2;
}


var int16View = new Int16Array(buffer);

for (var i = 0; i < int16View.length; i++) {
  console.log("Entry " + i + ": " + int16View[i]);
}

```

*  C 언어 구조체와 작업
```c
  struct someStruct {
  unsigned long id;
  char username[16];
  float amountDue;
};
```
```js
var buffer = new ArrayBuffer(24);

// ... 버퍼 내의 데이터를 읽어들임 ...

var idView = new Uint32Array(buffer, 0, 1);
var usernameView = new Uint8Array(buffer, 4, 16);
var amountDueView = new Float32Array(buffer, 20, 1);
```

**[⬆ 목차](#목차)**

---

## DOM and Layout Trees
...
**[⬆ 목차](#목차)**

---

## Factories and Classes
### Class로 구현한 ToDo Model
```js
class TodoModel {
    constructor(){
        this.todos = [];
        this.lastChange = null;
    }
    
    addToPrivateList(){
        console.log("addToPrivateList"); 
    }
    add() { console.log("add"); }
    reload(){}
}
```
### Factory function으로 구현한 ToDo Model
```js
function TodoModel(){
    var todos = [];
    var lastChange = null;
        
    function addToPrivateList(){
        console.log("addToPrivateList"); 
    }
    function add() { console.log("add"); }
    function reload(){}
    
    return Object.freeze({
        add,
        reload
    });
}
```
### Encapsulation
*  Class의 모든 멤버, 필드, 메서드는 public이다.
```js
var todoModel = new TodoModel();
console.log(todoModel.todos);     //[]
console.log(todoModel.lastChange) //null
todoModel.addToPrivateList();     //addToPrivateList
```
*  Factory function는 메서드만 노출되고 나머지 다른 것들은 모두 보호된다.
```js
var todoModel = TodoModel();
console.log(todoModel.todos);     //undefined
console.log(todoModel.lastChange) //undefined
todoModel.addToPrivateList();     //todoModel.addToPrivateList is not a function
```
### this
*  class를 사용할 때는 this가 context를 잃는 문제가 있다.
```js
class TodoModel {
    constructor(){
        this.todos = [];
    }
    
    reload(){ 
        setTimeout(function log() { 
           console.log(this.todos);    //undefined
        }, 0);
    }
}
todoModel = TodoModel();
todoModel.reload();
```
*  위 문제는 callback에 화살표 함수를 사용하여 해결 할 수 있다.
```js
class TodoModel {
    constructor(){
        this.todos = [];
    }
    
    reload(){ 
        setTimeout(() => { 
           console.log(this.todos);    //undefined
        }, 0);
    }
}
todoModel = TodoModel();
todoModel.reload();
```
*  Factory function은 this를 사용하지 않기 때문에 문제가 없다.
```js
function TodoModel(){
    var todos = [];
        
    function reload(){ 
        setTimeout(function log() { 
           console.log(todos);        //[]
       }, 0);
    }
}
todoModel = TodoModel();
todoModel.reload();
```
**[⬆ 목차](#목차)**

---

## this, call, apply and bind
...
**[⬆ 목차](#목차)**

---

## new, Constructor, instanceof and Instances
### new
new 연산자를 통해 개발자는 user-defined object type와 생성자 함수가 있는 built-in object type의 인스턴스를 만들 수 있다.  
new 키워드는 다음을 수행한다.  

*  새로운 object가 만들어진다.
*  this를 이 object에 결합한다.
*  생성자 함수의 prototype object는 새 object의 ```__proto__``` property가 된다.
*  함수로부터 object를 리턴한다.

#### ES5 class
```js
function User(name, points) {
  this.name = name; 
  this.points = points;
}
User.prototype.increment = function(){
  this.points++;
}
User.prototype.login = function() {
  console.log(“Please login.”)
}

let user1 = new User(“Dylan”, 6);
user1.increment();
```
#### ES6 class
```js
class User {
  constructor(name, points) {
    this.name = name;
    this.points = points;
  }
  increment () {
    this.points++;
  }
  login () {
    console.log("Please login.")
  }
}

let user1 = new User("John", 12);
user1.increment();
```
#### 새 object를 new로 생성해야 하는 이유
````js
var userProfile = function(name, age) {
    this.userName = name;
    this.userAge = age;
    return this;
};

var user = userProfile('uyeong', 27);
console.log(user === window); // true
console.log(window.userName); // uyeong
console.log(window.userAge); // 27
delete user; // true
delete window.userName; // true
delete window.userAge; // true

var user = new userProfile('uyeong', 27);
console.log(user === window); // false
console.log(window.userName); // undefined
console.log(window.userAge); // undefined
console.log(user.userName); // uyeong
console.log(user.userAge); // 27
````

### instance
*  object는 현실 세계의 개체를 프로그래밍으로 표현한 것이다.
````js
var person = {
  name: 'Juan',
  age: 40,
  gender: 'male',
  greeting: function() {
    alert('Hi! I\'m ' + this.name + '.');
  }
};
````
*  이 object를 사용하기 위해 이 object의 instance를 생성해야 한다.
```js
var guy = new person();
````
*  위 명령어 실행으로 person type의 object를 저장할 수 있는 메모리가 할당 및 초기화 되고 이 instance를 참조 할 수 있는 guy 변수가 만들어 진다.

### instanceof
*  instanceof 는 비교 연산자이다.
*  해당 변수가 사용하고 있는 prototype의 chain을 두 번째 인자와 쭉 비교해서 true나 false를 리턴한다.
*  모든 object는 기본 object인 Object를 확장하기 때문에 instanceof Object는 true이다.
```js
var Person = function(){ 
    this.name = "unikys"; 
}; 

var inst = new Person(); 
inst instanceof Person; // === true 
inst instanceof Object; // === true 
typeof inst; // === 'object'
```
*  primitive type에는 사용할 수 없다.
```js
"foo" instanceof String; // === false 
"foo" instanceof Object; // === false 
true instanceof Boolean; // === false 
true instanceof Object; // === false 

[0,1] instanceof Array; // === true 
{0:1} instanceof Object; // === true 

var color1 = new String("red"); 
var color2 = "red"; 
color1 == color2; // === true 
color1 instanceof String; // === true 
color2 instanceof String; // === false
```

**[⬆ 목차](#목차)**

---

## Prototype Inheritance and Prototype Chain
### Prototype
![prototype_function](./img/prototype_function.jpg)
*  함수를 선언하면 위와 같이 function, prototype 2개의 객체가 생성된다.
*  이 두 객체는 서로 참조 가능한 property를 가지고 있다.
  *  function은 prototype을 통해 prototype 객체에 접근한다.
  *  prototype은 constructor를 통해 function 객체에 접근한다.
*  접근 뿐만이 아니라 변경도 가능하다.
*  function 스스로는 prototype의 property에 접근할 수 없다.
```js
function Foo (){}
Foo.prototype.proto_val = '원형 값';

Foo.prototype.constructor.construct_val = "생성자 값";

console.log(Foo.prototype.proto_val); //원형 값 을 출력
console.log(Foo.construct_val); //생성자 값 을 출력
console.log(Foo.proto_val); //?! undefined를 출력
```

![prototype_function_instance](./img/prototype_function_instance.jpg)
*  instance화 되면 prototype의 property가 접근 할 수 있는 공간에 복제된다.
```js
function Foo (){} //함수 선언
Foo.prototype.proto_val = "접근 할 수있다!!"; //Foo의 프로토타입을 설정

var foo_instance = new Foo();  //Foo의 인스턴스를 생성

console.log(foo_instance.proto_val); //접근 할 수있다!! 를 출력
```
*  instance 안의 property를 변경해도 ```__proto__``` 안의 property는 변하지 않는다.
```js
function Foo(){}

Foo.prototype.proto_val = 100;    //프로토타입 속성을 설정합니다.

var foo_instance = new Foo();  //Foo의 인스턴스를 생성합니다.

console.log(foo_instance.proto_val); //프로토타입값 100을 출력을 합니다.

foo_instance.proto_val -= 1;  // 인스턴스에서 proto_val을 1줄여봅니다.

console.log(foo_instance.__proto__.proto_val); //프로토타입의 값은 그대로입니다.
console.log(foo_instance.proto_val);  //하지만 인스턴스는 1이 줄은 99가 출력이 됩니다.
```

### Prototype Inheritance
![prototype_inheritance](./img/prototype_inheritance.jpg)
*  함수를 선언하는 순간 Object.prototype을 상속하게 된다.
*  prototype chain은 prototype이 다른 prototype을 참조하는 행위가 반복되는 것이다.
```js
Object.prototype.say = function(){
    console.log(this.greet); //Object의 프로토타입에 say라는 메서드를 추가합니다.
}

function Foo (){
    this.greet = "hello world";    // Foo 생성자에서 greet이라는 속성을 추가합니다.
}

var foo_instance = new Foo();     //인스턴스를 생성합니다.

foo_instance.say(); //hello world를 출력합니다.
```
1. instance 내에 say가 있는지 확인한다.  
2. 없다면 instance가 참조하는 prototype에 say가 있는지 확인한다.  
3. 없다면 prototype이 참조하는 prototype에 say가 있는지 확인한다.  
4. 이 과정을 반복하다가 null이 나오면 중단하고 say에 undefined를 할당한다.  
5. say를 찾을 경우 say를 호출한다.  

*  다른 객체끼리의 상속
```js
function Vehicle (){}

Vehicle.prototype.wheels = 4;
Vehicle.prototype.getWheels = function(){ //Vehicle의 프로토타입의 속성을 설정합니다.
    console.log(this.wheels);
}

function Bicycle(){
    this.wheels = 2;
}

Bicycle.prototype.__proto__ = Vehicle.prototype; //Bicycle의 프로토타입이  Vehicle의 프로토타입을 참조하게 합니다.

var bicycle = new Bicycle(); //객체를 생성합니다. 

bicycle.getWheels();  // 2를 출력합니다.
```
![object_vehicle_bicycle](./img/object_vehicle_bicycle.jpg)
1. getWheels method를 실행할 경우 instance bicycle 안에 해당 method가 없기 때문에 prototype Bicycle이 참조하는 Vehicle을 확인한다.  
2. prototype Vehicle 안에는 getWheels method가 있기 때문에 호출한다.  

**[⬆ 목차](#목차)**

---

## Object.create and Object.assign
### Object.create
*  주어진 prototype object와 property로 새로운 object를 만든다.
*  상속을 구현할 때 사용한다.
```
Object.create(prototype[, propertiesObject])
```
```js
function fruits() {
    this.name = 'fruit 1';
}

function apple() {
    fruits.call(this);
}

apple.prototype = Object.create(fruits.prototype);
const app = new apple();
console.log(app.name);  // "fruit 1"
```
### Object.assign
*  열거할 수 있는 하나 이상의 source object로부터 target object로 속성을 복사할 때 사용한다.
```js
var obj1 = { a: 10, b: 10, c: 10 };
var obj2 = { b: 20, c: 20 };
var obj3 = { c: 30 };

var new_obj = Object.assign({}, obj1, obj2, obj3);

console.log(new_obj);  // Object { a: 10, b: 20, c: 30 }
```
**[⬆ 목차](#목차)**

---

## map, reduce, filter
...
**[⬆ 목차](#목차)**

---

## Pure Functions, Side Effects and State Mutation
*  Pure Function(순수 함수)는 결정론적이다.
같은 입력에는 항상 같은 출력을 리턴한다.
```js
const add = (x, y) => x + y // A pure function
```
```js
const magicLetter = '*'
const createMagicPhrase = (phrase) => `${magicLetter}abra${phrase}` // An impure function
```
```js
const fetchLoginToken = externalAPI.getUserToken // An impure function
```
*  Side Effect란 함수 외부 시스템의 변경이다.
*  순수 함수는 side effect가 없다.
  *  함수는 외부 상태를 변경하거나 함수로 들어온 인자의 상태를 변경하지 않는다.  
  *  함수는 결과를 만들어 내기 위해서 인자에만 의존한다.
*  Mutation은 배열이나 object 같은 source element를 변경하거나 영향을 주는 것을 의미한다.
*  프로그램에서 변화를 주는 것이 적을수록 추적해야 할 부분이 적어지므로 프로그램이 더 간단해 진다.  
*  비순수 함수
```js
const cities = ['서울']

function addElement(array, element) {
  const newArray = array
  newArray.push(element)
  return newArray
}

const newCities = addElement(cities, '부산')
console.log(newCities) // [ '서울', '부산' ]
console.log(cities) // [ '서울', '부산' ]

const newCities2 = addElement(cities, '부산')
console.log(newCities2) // [ '서울', '부산', '부산' ]
console.log(cities) // [ '서울', '부산', '부산' ]
```
*  순수 함수로 변경
```js
function addElement(array, element) {
  const newArray = [...array]
  newArray.push(element)
  return newArray
}
```
**[⬆ 목차](#목차)**

---

## Closures
...
**[⬆ 목차](#목차)**

---

## High Order Functions
*  High Order Function(고차 함수)는 함수를 인자로 전달 받거나 함수를 결과로 반환하는 함수를 말한다.
*  고차 함수는 외부 상태 변경이나 가변(mutable) 데이터를 피하고 불변성(Immutability)을 지향하는 함수형 프로그래밍에 기반을 두고 있다.
```js
// 함수를 인자로 전달받고 함수를 반환하는 고차 함수
function makeCounter(predicate) {
  // 자유 변수. num의 상태는 유지되어야 한다.
  let num = 0;
  // 클로저. num의 상태를 유지한다.
  return function () {
    // predicate는 자유 변수 num의 상태를 변화시킨다.
    num = predicate(num);
    return num;
  };
}

// 보조 함수
function increase(n) {
  return ++n;
}

// 보조 함수
function decrease(n) {
  return --n;
}

// makeCounter는 함수를 인수로 전달받는다. 그리고 클로저를 반환한다.
const increaser = makeCounter(increase);
console.log(increaser()); // 1
console.log(increaser()); // 2

// makeCounter는 함수를 인수로 전달받는다. 그리고 클로저를 반환한다.
const decreaser = makeCounter(decrease);
console.log(decreaser()); // -1
console.log(decreaser()); // -2
```
**[⬆ 목차](#목차)**

---

## Recursion
...
**[⬆ 목차](#목차)**

---

## Collections and Generators
*  자바스크립트에는 다음과 같은 데이터 컬렉션이 있다.
  *  Indexed Collection : Arrays, Typed Array
  *  Keyed Collection : Objects, Map, Set, Weak Map, Weak Set
*  ES6에서 추가된 컬렉션 : Typed Array, Map, Set, Weak Map, Weak Set
### Set
*  Set은 value를 key값으로 갖는 컬렉션이다.
*  Set은 값의 추가, 삭제 등 수정이 가능하다.
*  Set은 값이 중복되지 않는다.
#### Set 메서드 사용예  
*  size : 크기
*  has : 값 확인
*  add : 값 추가
*  delete : 값 삭제
*  forEach : 반복자
*  clear : 모든 값 삭제
```js
let animals = new Set();

animals.add('🐷');
animals.add('🐼');
animals.add('🐢');
animals.add('🐿');
console.log(animals.size); // 4
animals.add('🐼');
console.log(animals.size); // 4

console.log(animals.has('🐷')); // true
animals.delete('🐷');
console.log(animals.has('🐷')); // false

animals.forEach(animal => {
  console.log(`Hey ${animal}!`);
});

// Hey 🐼!
// Hey 🐢!
// Hey 🐿!

animals.clear();
console.log(animals.size); // 0
```
#### array를 사용한 Set 초기화
```js
let myAnimals = new Set(['🐷', '🐢', '🐷', '🐷']);

myAnimals.add(['🐨', '🐑']);
myAnimals.add({ name: 'Rud', type: '🐢' });
console.log(myAnimals.size); // 4

myAnimals.forEach(animal => {
  console.log(animal);
});


// 🐷
// 🐢
// ["🐨", "🐑"]
// Object { name: "Rud", type: "🐢" }
```
#### string을 사용한 Set 초기화
```js
console.log('Only unique characters will be in this set.'.length); // 43

let sentence = new Set('Only unique characters will be in this set.');
console.log(sentence.size); // 18
```
#### for...of를 사용한 loop
```js
let moreAnimals = new Set(['🐺', '🐴', '🐕', '🐇']);

for (let animal of moreAnimals) {
  console.log(`Howdy ${ animal }`);
}

// Howdy 🐺
// Howdy 🐴
// Howdy 🐕
// Howdy 🐇
```
#### keys와 values 메서드(동일한 기능)
```js
let partyItems = new Set(['🍕', '🍾', '🎊']);
let items = partyItems.values();

console.log(items.next());
console.log(items.next());
console.log(items.next());
console.log(items.next().done);

// Object {
//   done: false,
//   value: "🍕"
// }

// Object {
//   done: false,
//   value: "🍾"
// }

// Object {
//   done: false,
//   value: "🎊"
// }

// true
```
**[⬆ 목차](#목차)**
### Map
*  Map은 Key - Value 쌍으로 이루어진 컬렉션이다.
*  Map은 object와 다르게 모든 타입을 key로 사용할 수 있다(object와 function까지도...)
#### Map 메서드 사용예  
*  size : 크기
*  has : 값 확인
*  set : 값 추가
*  get : 값 가져오기
*  delete : 값 삭제
*  clear : 모든 값 삭제
```js
let things = new Map();

const myFunc = () => '🍕';

things.set('🚗', 'Car');
things.set('🏠', 'House');
things.set('✈️', 'Airplane');
things.set(myFunc, '😄 Key is a function!');

things.size; // 4

things.has('🚗'); // true

things.has(myFunc) // true
things.has(() => '🍕'); // false, not the same reference
things.get(myFunc); // '😄 Key is a function!'

things.delete('✈️');
things.has('✈️'); // false

things.clear();
things.size; // 0

// setting key-value pairs is chainable
things.set('🔧', 'Wrench')
      .set('🎸', 'Guitar')
      .set('🕹', 'Joystick');

const myMap = new Map();

// Even another map can be a key
things.set(myMap, 'Oh gosh!');
things.size; // 4
things.get(myMap); // 'Oh gosh!'
```
#### Map을 array로 초기화
```js
const funArray = [
  ['🍾', 'Champagne'],
  ['🍭', 'Lollipop'],
  ['🎊', 'Confetti'],
];

let funMap = new Map(funArray);
funMap.get('🍾'); // Champagne
```
#### Map 반복자 
*  for...of와 array destructuring을 통해
```js
let activities = new Map();

activities.set(1, '🏂');
activities.set(2, '🏎');
activities.set(3, '🚣');
activities.set(4, '🤾');

for (let [nb, activity] of activities) {
  console.log(`Activity ${nb} is ${activity}`);
}

// Activity 1 is 🏂
// Activity 2 is 🏎
// Activity 3 is 🚣
// Activity 4 is 🤾
```
*  forEach를 통해
```js
activities.forEach((value, key) => {
  console.log(`Activity ${key} is ${value}`);
});
```
### WeakSet, WeakMap
*  자바스크립트의 garbage collection은 더 이상 참조되지 않는 object가 자동으로 삭제되고 그 resource를 되찾는 메모리 관리 형태이다.
*  Map과 Set의 object 참조는 강하게 결합되어 있어 garbage collection을 허용하지 않는다.
*  WeakSet과 WeakMap은 더 이상 필요하지 않는 object를 메모리에서 지울 수 있다.
*  Weak 컬렉션은 일반 컬렉션과 사용법은 비슷하지만 사용 가능한 메서드 수가 적다.
*  WeakSet 사용예
```js
const yesdoing = new WeakSet(); // WeakMap을 생성합니다. 
const age = {}; // 값은 반드시 객체여야 합니다. 

yesdoing.add(age); // 값을 추가합니다.

yesdoing.has(age); // True
yesdoing.delete(age) // 값을 삭제합니다.
```
*  WeakMap 사용예
```js
const yesdoing = new WeakMap(); // WeakMap을 생성합니다. 
const age = {}; // 키는 반드시 객체여야 합니다.
const job = {}; // 키는 반드시 객체여야 합니다.

yesdoing.set(age, 11111); // 키 - 값을 설정합니다.
yesdoing.set(job, 'air'); // 값으로는 어떤 타입이라도 들어올 수 있습니다. 

yesdoing.has(job); // True
yesdoing.delete(job) // key를 삭제합니다.
```
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
