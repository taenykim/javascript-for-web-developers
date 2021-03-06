# 언어의 기초

이번 챕터에서는 자바스크립트 언어에서의 타입, 연산, 문장들에 대해서 간단하게 알아보았다. 기존에 아는 내용은 넘어가고 새로 배운내용이나 정리할만한 내용 위주로 기록했는데 양이 상당하다.

[1. 변수명 짓기](#1-변수명-짓기) / [2. 세미콜론](#2-세미콜론)

[3. data Type](#3.-data-Type) / [4. [type 1]. undefined](#4-type-1-undefined) / [5. [type 2]. null](#5-type-2-null) / [6. [type 3]. boolean](#6-type-3-boolean) / [7. [type 4]. 숫자](#7-type-4-숫자) / [8. [type 5]. 문자열](#8-type-5-문자열) / [9. [type 6]. 객체](#8-type-5-문자열)

[10. 단항연산자](#10-단항연산자) / [11. [불리언 연산자 1]. ! (NOT)](#11-불리언-연산자-1--not) / [12. [불리언 연산자 2]. && (AND)](#12-불리언-연산자-2--and) / [13. [불리언 연산자 3.] || (OR)](#13-불리언-연산자-3--or)

[14. 숫자와 문자의 덧셈과 뺄셈](#14-숫자와-문자의-덧셈과-뺄셈)

[15. 관계 연산자(>,<)](#15-관계-연산자) / [16. 동일 연산자(==), 일치 연산자(===)](#16-동일-연산자-일치-연산자)

[17. for...in vs for...of](#17-forin-vs-forof) / [18. 문장 레이블, break, continue](#18-문장-레이블-break-continue)

[19. 함수의 매개변수](#19-함수의-매개변수)

## 1. 변수명 짓기

변수명(식별자)를 지을 때, 지켜야할 규칙이 있다.

1. 첫번 째 문자는 `글자` 혹은 `_`, `$` 만 가능하다.

```js
const 1num; // x
const num1 // o

const _name; // o
const $name; // o
```

2. 예약어는 변수명으로 불가능.

```js
const true; // x
const case; // x
// ...
```

3. 카멜케이스, 스네이크케이스 (option)

```js
let myname = 'taeeun' // bad
let myName = 'taeeun' // good

const MAXLENGTH = 10 // bad
const MAX_LENGTH = 10 // good
```

> 카멜케이스(대문자사용), 스네이크케이스(언더바사용) 을 혼용해서 사용한다고 한다.

## 2. 세미콜론

책에서는 세미콜론을 항상 쓰는 것을 권장하지만, 인터넷을 찾아보니 세미콜론을 쓰지 않아도 된다는 글도 있었다.

- 참고 글 : [https://bakyeono.net/post/2018-01-19-javascript-use-semicolon-or-not.html](https://bakyeono.net/post/2018-01-19-javascript-use-semicolon-or-not.html)

세미콜론을 쓰지 않아도 되는 이유는 인터프리터가 **문장의 끝이라고 생각되는 지점**에 세미콜론을 자동으로 붙여주기 때문이다. 이 기능을 세미콜론 자동 삽입(**ASI**, automatic semicolon insertion)이라고 한다.

책에서는 세미콜론을 붙이지 않았을 때의 문제를 다음과 같은 예시를 들어 설명한다.

```js
function returnObject() {
    return
    {
        a:1,
        b:2
    }
}
```

위 코드는 인터프리터가 ASI를 통해 다음과 같이 인식해서 `undefined`를 return 하게 된다.

```js
function returnObject() {
    return;
    {
        a:1,
        b:2
    };
}
```

하지만, 다음과 같이 짜면 정상적으로 인식한다.

```js
function returnObject() {
  return {
    a: 1,
    b: 2,
  }
}
```

그리고 해당 글에서는 세미콜론을 넣지 않아도 된다는 데서 더 나아가, 세미콜론을 쓰지 말아야 한다고 주장하는 이유에 대해 설명한다. ASI 방식을 이해하고 그에 맞는 코딩스타일을 정립하면 세미콜론을 넣을 필요가 없고, 오히려 세미콜론을 넣는 규칙을 신경쓰는 것이 더 성가실 수도 있다는 것이다.

```js
class Foo {
  constructor() {
    if (baz) {
      return 42 // ok
    } // <– AVOID!
    return 12 // ok
  } // <– AVOID!
} // <– AVOID!
```

그리고 ASI가 일을 방해하지 않도록 하려면 딱 한 가지 규칙만 기억하면 된다고 한다. 그것은 바로 행의 시작을 `\[`, `\(`, `\``으로 하지 않는 것이다. 꼭 그렇게 해야 한다면, 다음과 같이 세미콜론으로 행을 시작하면 된다고 한다.

```js
;[1, 2, 3].forEach(bar)
```

이를 피하기 위해서 값을 변수안에 집어넣거나 `const numbers = [].forEach()` 값을 return 해줄 수도 있다. `return [].forEach()`

## 3. data Type

자바스크립트 데이터 타입은 총 7개로 원시타입 6개, 참조타입 1개로 이루어져있다.

| 원시타입  | 참조타입 |
| --------- | -------- |
| undefined | Object   |
| null      |          |
| boolean   |          |
| number    |          |
| string    |          |
| symbol    |          |

> symbol은 ECMAScript 6에서 추가되었음. 이번 챕터에서 언급은 x

## 4. [type 1]. undefined

변수를 선언하고 초기화시켜주지 않으면 해당 변수는 자동으로 **undefined** 값을 할당받는다.

이 값은 빈 값(`null`)이 아니며 실제로는 Garbage 값을 가지고 있다고 한다.

```js
let message
typeof message
// "undefined"
```

추가로 호이스팅시에도 , 변수에 자동으로 **undefined** 값을 할당받는다. `var`

```js
console.log(message) // undefined
var message = 'hi'
```

하지만 let,const 키워드를 사용하면 **undefined**를 할당하기 전에 호출하기 때문에 error를 출력한다. `let, const`

```js
console.log(message) // error
let message

let message
console.log(message) // undefined
```

> 이를 TDZ라고 함. 변수를 읽긴하였지만 `undefined` 를 아직 할당하지 않은 상태

## 5. [type 2]. null

**null**은 빈 값을 의미하며 정확히는 **빈 객체**를 가리킨다. 그렇기 때문에 typeof 연산자를 썼을 때 null일 경우, object를 반환한다.

```js
let car = null
typeof car
// "object"
```

`null==undefined` 는 true를 출력하지만 `null===undefined` 는 false 를 출력함.

## 6. [type 3]. boolean

**boolean** 은 true, false 두가지 값만 가지는 타입이다. 하지만 Boolean() 함수를 호출해서 다른 타입을 boolean 타입으로 변환시킬 수도 있고, if문 같은 제어문에서는 타입들이 자동으로 boolean으로 변환된다.

| type        | true      | false        |
| ----------- | --------- | ------------ |
| `undefined` |           | undefined    |
| `null`      |           | null         |
| `숫자`      | 0빼고 다  | 0,NaN        |
| `문자열`    | ''빼고 다 | ''(빈문자열) |
| `객체`      | 다        | null         |

정리하면, undefined, null, 0, NaN, '' 제외하고 모두 **true** !!

> {} 도 true !! 헷갈리지 않기!

## 7. [type 4]. 숫자

일반적으로 숫자를 변수에 할당하면 **10진법**의 숫자가 변수에 담긴다.

하지만, 앞자리에 `0` (8진법), `0x` (16진법)을 붙이면 각각 8진법, 16진법의 숫자를 할당할 수도 있다. 하지만 다음 각각의 숫자들이 해당진법의 숫자를 넘지 않아야함.

```js
// 8진법
let num = 070 // 56

// 9가 8진법을 넘으므로, 10진법으로 출력됨
let num = 079 // 79
```

```js
let num = 0xa // 10

// 대소문자는 가리지 않는다.
let num = 0xf // 15
```

부동소수점 숫자인 경우, 사칙연산할 때 주의해야함! 정수인 경우, 정확한 계산이 되지만, 부동소수점 숫자는 부정확하다.

```js
if (1 + 1 == 2) console.log('true')
// true

if (1.5 + 0.5 == 2) console.log('true')
// true를 출력 하지 않음 (2.000000000004)
```

NaN은 숫자의 값 중 하나로, 숫자로 변환할 수 없는 경우 반환되는 값이다.

```js
isNaN(NaN) // true
isNaN('blue') // true

isNaN(10) // false : 10
isNaN('10') // false : 10
isNaN(true) // false : 1
isNaN(false) // false : 0
```

즉, 자바스크립트에서는 숫자가 아니지만 숫자로 변환할 수 있는 타입끼리의 연산은 자동으로 변환해서 연산을 수행한다.

```js
console.log('6' - '1') // 5
console.log(true * 3) // 3

// 예외적으로 문자열 + 문자열은 문자열로서 더하기를 수행함
console.log('5' + '5' == '55') // true, 10이 아님!
```

추가로, 자바스크립트에서는 0으로 나누는 것이 허용된다. 하지만 숫자가 아닌 값이나 0을 0으로 나눌 경우 NaN을 출력한다.

```js
console.log(1 / 0) // Infinity
console.log(1 / -0) // -Infinity

console.log('숫자가 아님' / 0) // NaN
console.log(0 / 0) // NaN
```

그리고 숫자가 아닌 값을 숫자로 바꾸는 함수는 대표적으로 세가지이며 `+`를 붙이는 방식도 있다.

| 변환방식     | 설명                                                                                                                                            |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Number()     | 리딩제로(숫자 앞에 붙이는 0)을 무시함.(16진법 제외) 그렇기 때문에 8진법 표기법(070)은 모두 10진법으로 변환되지만 16진법 표기법(0xA)는 잘 표기됨 |
| parseInt()   | 마찬가지 리딩제로 무시함.(16진법 제외) 문자열의 경우, 숫자가 아닌 문자가 나올 때까지 변환. 부동소수점은 버림. 두번째 인자로 x진법 변환 가능     |
| parseFloat() | 리딩제로 **항상** 무시함. (16진법 포함)                                                                                                         |
| +(값 앞에)   | 값 앞에 +를 붙이면 숫자타입으로 변환                                                                                                            |

```js
Number('1234dd') // NaN
Number('070') // 70

parseInt('1234dd') // 1234
parseInst('12dd34dd') // 12
parseInt('070') // 70
parseInt('70', 8) // 56

parseFloat('123.45.6') // 123.45
parseFloat('0xA') // 0

let num = '123'
typeof num // string
typeof +num // number
```

x진법의 수(로변환 가능한 값)을 10진법으로 변환할 때는 `parseInt`, 10진법의 수를 x진법의 문자열로로 고칠 경우에는 `toString` 메소드를 사용하면 된다.

```js
let num = 70
num.toString(2) // "1000110"

parseInt('1000110', 2) // 70
```

## 8. [type 5]. 문자열

문자열 내부에서 특수문자는 보통 `\`기호를 이용해서 사용한다.

> 책에서는 [[리터럴(literal)](https://ko.wikipedia.org/wiki/%EB%A6%AC%ED%84%B0%EB%9F%B4) : 소스 코드의 고정된 값을 대표하는 용어]라고 정의함

| 리터럴 | 의미                                      |
| ------ | ----------------------------------------- |
| \n     | 줄바꿈                                    |
| \t     | 탭                                        |
| \b     | 백스페이스                                |
| \xnn   | 16진수 코드(\x41 : A)                     |
| \unnnn | UTF-16 인코딩 규칙을 사용하는 16진수 코드 |

그리고 문자열은 **불변성**의 성질을 가지고 있어서 문자열 자체를 바꿀 수 없고, 해당 문자열 변수에 새로운 값을 할당하는 방식으로 값을 바꾸어야 함.

```js
let str = 'hot'
str[0] = 'p' // 변화없음

str = 'p' + str.slice(1) // good
str = str.replace('h', 'p') // good

// 이런식으로 새로 할당해주어야됨.
```

그리고 문자가 아닌 값을 문자열로 변환방법은 대표적으로 두가지이며 `""`를 더하는 방식도 있다.

| 변환방식   | 설명                                                       |
| ---------- | ---------------------------------------------------------- |
| String()   | null, undefined같은 toString 메소드가 없는 값들도 변환가능 |
| toString() | 인자에 들어가는 값 x에 따라 x진법의 수로 변환 가능         |
| (값)+ ""   | ""를 더해주면 문자열로 변환됨                              |

```js
let value = null
String(value) // "null"
value.toString() // error

let num = 5
let value = num + ''
typeof value // string
```

## 9. [type 6]. 객체

ECMAScript 에서 객체는 데이터와 기능의 집합을 의미한다.

```js
const obj = new Object()
const arr = new Array()
const func = new Function()
```

> 의문! 배열,함수,객체인스턴스 모두 객체인가?? 5장부터 객체가 나오긴하는데 객체의 정의가 {}만 말하는 것인지 Array, Function, Date, console 이런 내장객체를 포괄하는 개념인지 헷갈림.. 그냥 원시타입 아닌 것들은 전부 다 객체인가? [참고링크](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects)

참고링크 : [빌트인 객체](https://poiemaweb.com/js-built-in-object)
![](https://poiemaweb.com/img/objects.png)

내가 원래 알고있는 객체랑 링크에 나오는 전체를 포괄하는 개념의 객체(그림 맨 왼쪽 노란박스의 Object)가 달라서 헷갈렸던 것 같다.

내가 원래 알고 있던 객체의 의미는

```js
var obj = {
  name: 'taeeun',
  age: 27,
}
```

이건데, 이건 위 이미지에서 native Object 안의 Object만 의미하는 게 아닌가 생각했다.

근데 생각해보니까

```js
var obj = {
  // 속성
  property: 'property',

  // 메소드
  method: function () {},
}
```

객체는 이런 식으로 프로퍼티(속성)과 메소드를 추가하여 독립된 새로운 객체를 만들 수 있다. 이렇게 생각하니까 전역객체인 `window`나 내장객체인 `Array`같은 것들이 다 객체다 라는 말이 이해가 되었다.

그리고 찾아보니까 `JavaScript에서 모든 객체들은 Object의 자손입니다.`[MDN 참고링크](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object)라는 말이 있는데 위 그림의 모든 것을 포괄하는 의미의 객체(맨 왼쪽 노란박스의 Object)랑 native Object 안에 있는 Object랑 같은 거라고 볼수 있을까?

프로토타입 상속을 공부할 때 정확하게 이해할 수 있을거 같다.

new 키워드를 통하여 인스턴스를 만들 수도 있다.

```js
function User(name) {
  this.name = name
  this.isAdmin = false
}

let user = new User('Jack')

console.log(user.name) // Jack
console.log(user.isAdmin) // false
```

> 의문! 우리가 사용하는 함수나 배열도 다 new 를 이용해서 객체 인스턴스화 시켜서 만든것? 그렇다면 `Array`, `Function` 이런 애들을 내장객체라고 부르는데 그로 인해 생성된 인스턴스도 객체인데 객체로 객체를 만든건가..?

이것도 마찬가지로 프로토타입 상속 공부할 때 정확히 이해할 수 있을거 같다.

```js
// 배열의 경우
let arr = [1, 2, 3, 4]
let arr = new Array(1, 2, 3, 4)

// 함수의 경우
let func = function () {}
let func = new Function()
```

## 10. 단항연산자

증감 연산자 `++`, `--` 는 값 앞뒤로 붙일 경우, 현재 값에서 1을 더하거나 빼며, 단항 플러스, 단항 마이너스 연산자 `+`, `-`는 각각 값을 숫자로 변환하거나 숫자의 부호를 바꿀 때 사용한다.

> 증감 연산자의 경우, 헷갈릴 수 있기 때문에 이해하고서 실제 사용은 지양하자! (실수하기 쉽고 의미를 정확하게 판단할 수 없는 코드를 좋은 코드라고 말하기 어렵다고 책에서는 언급한다.)

```js
let num1 = 2
let num2 = 20
let num3 = --num1 + num2 // 21
let num 4 = num1 + num2 // 21
// 값의 앞에 붙은 증감연산자는 값이 적용된 후 식을 수행함

let num1 = 2
let num2 = 20
let num3 = num1-- + num2 // 22
let num 4 = num1 + num2 // 21
// 값의 뒤에 붙은 증감연산자는 식을 수행한 후 값을 적용 함.

let answer = 5
answer++
console.log(answer) //6
// 이렇게 한 라인에 써주는 것은 헷갈릴 일이 없음.
```

## 11. [불리언 연산자 1]. ! (NOT)

앞에서 언급했듯이, if문 같은 제어문에서는 타입들이 자동으로 boolean으로 변환된다. 하지만 조건문이 없어도 !! 두번 써주면 해당 값의 boolean 값을 가져올 수 있다.

```js
!false // true
!'blue' // false

if ('blue') console.log('true') // true

!!'blue' // true
Boolean('blue') // true
!!0 // false
Boolean(0) // false
```

## 12. [불리언 연산자 2]. && (AND)

| 피연산자1 | 피연산자2 | 결과 |
| --------- | --------- | ---- |
| 0         | null      | 0    |
| 0         | 1         | 0    |
| 1         | 0         | 0    |
| 1         | {}        | {}   |

위 표를 보면 첫번째 피연산자가 false 일 경우, 첫번째 피연산자를 반환하고,

첫번째 피연산자가 true 일 경우, 두번째 피연산자를 반환하는 것을 볼 수 있다.

즉, &&을 이런 식으로도 사용할 수 있다.

```js
// 일반적인 용법
if (1 && {}) return true

// 검증(?)의 용법
obj && obj.method()
```

obj라는 객체의 메소드를 사용하고자 할 때, obj라는 객체가 없을 경우, 메소드에 접근할 수 없기 때문에 에러를 뱉는다. 하지만 obj가 있을 때만 해당 메소드를 실행하게끔 `&&`로 끊어줄 수 있다.

> 책에서의 found && someUndeclaredVariable 을 변형하였음.

## 13. [불리언 연산자 3.] || (OR)

| 피연산자1 | 피연산자2 | 결과 |
| --------- | --------- | ---- |
| 0         | null      | null |
| 0         | 1         | 1    |
| 1         | 0         | 0    |
| 1         | {}        | 1    |

위 표를 보면 첫번째 피연산자가 false 일 경우, 두번째 피연산자를 반환하고,

첫번째 피연산자가 true 일 경우, 첫번째 피연산자를 반환하는 것을 볼 수 있다.

> && 와 다르게 true가 존재하면 바로 그 값을 반환하는 것을 알 수 있다.

즉, ||을 이런 식으로도 사용할 수 있다.

```js
// 일반적인 용법
if (0 || null || undefined || 1) return true

// 백업(?)의 용법
let obj = preferredObject || backupObject
```

obj라는 객체의 값을 할당할 때, preferredObject를 담을 목적이지만, 해당 값이 빈값이거나 할당이 안된 값이면(false) null이나 undefined를 할당하는 것이 아니라 backupObject 값을 할당하게끔 할 수 있다.

## 14. 숫자와 문자의 덧셈과 뺄셈

앞서서 자바스크립트에서는 숫자가 아니지만 숫자로 변환할 수 있는 타입끼리의 연산은 자동으로 변환해서 연산을 수행한 다는 것을 배웠다.

```js
console.log('6' - 1) // 5
console.log(true * 3) // 3

// 예외적으로 문자열 + 문자열은 문자열로서 더하기를 수행함
console.log('5' + '5' == '55') // true, 10이 아님!
console.log('5' + 5 === '55') // 마찬가지로 true, 10이 아님!
```

실수를 피하기 위해서는 문자열 출력과 숫자 연산을 같이하지 않거나, 타입 변환을 잘 해주는 것이 중요하다.

```js
let num1 = 10
let num2 = 20
let message = 'The sum of 10 + 20 is ' + num1 + num2 // The sum of 10 + 20 is 1020
let message = 'The sum of 10 + 20 is ' + (num1 + num2) // The sum of 10 + 20 is 30

// best
let result = num1 + num2
let message = 'The sum of 10 + 20 is ' + result // The sum of 10 + 20 is 30
```

## 15. 관계 연산자(>,<)

| 피연산자 상태                    | 비교방식                                                    |
| -------------------------------- | ----------------------------------------------------------- |
| 모두 숫자                        | 숫자형 비교                                                 |
| 모두 문자열                      | 문자열 비교(맨 앞자리부터 문자코드 비교, 대소문자도 고려함) |
| 하나만 숫자                      | 다른 피연산자를 숫자로 변환 후 숫자형 비교                  |
| 하나만 숫자(다른 피연산자가 NaN) | 항상 false                                                  |

```js
'Brick' < 'alphabet' // true
'Brick'.toUpperCase() > 'alphabet'.toUpperCase() // true
'23' < '3' // true
'23' > 3 // true

'a' > 3 // false
'a' <= 3 // false
```

## 16. 동일 연산자(==), 일치 연산자(===)

동일 연산자는 `"2" == 2` 처럼 자바스크립트의 타입 변환을 통해 일치할 수 있는 관계이며, 일치 연산자는 `"2" === "2"` 처럼 값과 타입이 모두 일치할 때를 가리킨다.

```js
null == undefined // true

typeof null // object
typeof undefined // undefined

null === undefined // false

true == 1 // true
true == 2 // false
true === 1 // false

'2' == 2 // true
'2' === 2 // false
```

> 여러가지 문제를 피해가 위해서 동일 연산자(==) 보다는 일치 연산자(===)를 쓰는 것이 권장됨.

## 17. for...in vs for...of

| 용법     | 특징                                       |
| -------- | ------------------------------------------ |
| for...in | 객체, 배열 모두 사용가능 / 프로퍼티 가져옴 |
| for...of | 배열만 가능(객체는 안됨) / 값 가져옴       |

for...in 이 더 범용성이 높고 프로퍼티를 통해 값을 가져올 수 있으니 for...of를 쓸 일은 없을 것 같다.

```js
let iterable = [3, 5, 7]
iterable.foo = 'hello'

// good
for (let i in iterable) {
  console.log(i) // 0, 1, 2, "foo"
}

// bad
for (let i of iterable) {
  console.log(i) // 3, 5, 7
}

// good
for (let i in iterable) {
  console.log(iterable[i]) // 3, 5, 7, "hello"
}
```

배열처럼 순서가 없는 객체에서도 프로퍼티, 값 탐색 가능!

```js
let obj = {
  name: 'taeeun',
  age: 27,
  hobby: 'movie',
}

for (let i in obj) {
  console.log(i) // name, age, hobby
}

for (let i in obj) {
  console.log(obj[i]) // 'taeeun', 27, 'movie'
}
```

## 18. 문장 레이블, break, continue

for문 같은 문장에 `label:statement` 이런 식으로, 레이블을 붙여서 break와 continue 시, 참조할 수 있다.

```js
// contine 레이블

loop1: for (let i = 0; i < 3; i++) {
  //첫번째 for문은 "loop1" 레이블을 붙였다.
  loop2: for (let j = 0; j < 3; j++) {
    //두번째 for문은 "loop2" 레이블을 붙였다.
    if (i === 1 && j === 1) {
      continue loop1
    }
    console.log('i = ' + i + ', j = ' + j)
  }
}

// 출력 결과:
//   "i = 0, j = 0"
//   "i = 0, j = 1"
//   "i = 0, j = 2"
//   "i = 1, j = 0"
//   "i = 2, j = 0"
//   "i = 2, j = 1"
//   "i = 2, j = 2"
```

```js
// break 레이블

loop1: for (let i = 0; i < 3; i++) {
  //첫번째 for문은 "loop1" 레이블을 붙였다.
  loop2: for (let j = 0; j < 3; j++) {
    //두번째 for문은 "loop2" 레이블을 붙였다.
    if (i === 1 && j === 1) {
      break loop1
    }
    console.log('i = ' + i + ', j = ' + j)
  }
}

// 출력 결과:
//   "i = 0, j = 0"
//   "i = 0, j = 1"
//   "i = 0, j = 2"
//   "i = 1, j = 0"
```

> continue는 성능문제를 일으켜서 최대한 사용을 권장하지 않는다고 한다. 중첩을 돌면서 해당 조건을 만족하면 return 이나 break로 재빨리 반복문을 빠져나오게끔하는 코드가 좋은 코드일 듯!

## 19. 함수의 매개변수

ECMAScript의 함수의 매개변수는 다른 언어의 매개변수와 다르게 **매개변수의 숫자를 따지지 않으며**, **데이터 타입도 체크하지 않는다**. 즉, 함수에서 매개변수를 두 개 받도록 만들었더라도 반드시 매개변수를 두 개 넘겨야 하는 것이 아니며, 한 개, 세 개, 또는 아예 넘기지 않아도 된다. 이는 ECMAScript의 매개변수가 내부적으로 **배열** 로 표현되기 때문이다. 이 배열 내부에서는 어떤 값이 들어있는지(타입이 같든 다르든) 체크하지 않는다.

그리고 함수는 arguments 라는 객체를 갖는데, 이 객체를 통해 매개변수의 값에 접근할 수 있다.

```js
function sayHi(name, message) {
  console.log('Hello ' + name + ',' + message)
}
sayHi('taeeun', 'welcome')

// same

function sayHi() {
  console.log('Hello ' + arguments[0] + ',' + arguments[1])
}
sayHi('taeeun', 'welcome')
```

즉, 이런식으로 매개변수의 길이를 반영하는 함수도 작성이 가능하다.

```js
function add() {
  let sum = 0
  for (let i = 0; i < arguments.length; i++) {
    sum += arguments[i]
  }
  console.log(sum)
}

add(1) // 1
add(1, 2, 3, 4, 5) // 15
```

> p.104 페이지에 "ECMAScript의 매개변수는 모두 값으로 넘겨야 합니다. 매개변수를 참조 형식으로 전달할 수는 없습니다." 라는 말은 이해안됨.ㅠ

참고링크 : [https://www.javascripttutorial.net/javascript-pass-by-value/](https://www.javascripttutorial.net/javascript-pass-by-value/)

```js
// 이건 참조값을 변화시켜서 잘 동작함
let arr = [1, 2, 3]
function a(k) {
  k.splice(0, 1)
  console.log(k)
}
a(arr) // [2,3]
console.log(arr) // [2,3]
```

```js
// 이건 함수 내부 변수만 다른 값을 가리키기 때문에 잘 작동안함
let arr = [1, 2, 3]
function a(k) {
  k = [2, 3]
  console.log(k)
}
a(arr) // [2,3]
console.log(arr) // [1,2,3]
```

마찬가지로 자바스크립트는 자바처럼 오버로딩은 없지만 매개변수가 배열로 들어온다는 성질을 이용해서 오버로딩을 흉내낼 수 있다.

## 참고

[https://bakyeono.net/post/2018-01-19-javascript-use-semicolon-or-not.html](https://bakyeono.net/post/2018-01-19-javascript-use-semicolon-or-not.html)

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures](https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures)

[https://ko.javascript.info/constructor-new](https://ko.javascript.info/constructor-new)

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects)

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of)

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/label](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/label)
