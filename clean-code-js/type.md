# type

## javascript에서 타입 검사하기

```js
typeof '문자열' // 'string'
typeof true // 'boolean'
typeof undefined // 'undefined'
typeof 123 // 'number'
typeof Symbol() // 'symbol'

// 함수처럼 사용도 가능하다
typeof (true) // 'boolean'
```

- `typeof` 로 모든 값을 처리할 수 없다.

## PRIMITIVE vs REFERENCE

```js
function myFunc() {}
class MyClass {}
const str = new String('문자열')

typeof myFunc // 'function'
typeof MyClass // 'function'
typeof str // 'object'
// javascript의 오류
typeof null // 'object'
```

### instanceof

```js
function Person(name, age) {
  this.name = name;
  this.age = age
}

const juhwan = new Person('juhwan', 20)
const person = {
  name: 'juhwan',
  age: 20
}

juhwan instanceof Person // true
person instanceof Person // false

const arr = []
const func = function() {}
const date = new Date()

arr instanceof Array // true
func instanceof Function // true
date instanceof Date // true

arr instanceof Object // true
func instanceof Object // true
date instanceof Object // true
```

#### 해결책

```js
const date = new Date()

// Wrapper 객체까지 감시 가능
Object.prototype.toString.call(new String('')) // '[object String]'
Object.prototype.toString.call(date) // '[object Date]'
```

- 검색할 때, 최신 자료를 확인해 보는 습관을 가지자

## undefined & null

![undefined-null](/assets/undefined-null.png)

- undefined란 기본값
- undefined와 null에 대한 팀에서 컨벤션이 있는 것이 좋다

```js
!null // true
!!null // false

null === false // false
!null === true // true

// null => math => 0
null + 123 // 123
```

- undefined, null: 값이 없거나 정의되지 않은 명시적인 표현
  - undefined: NaN에 가깝고, type은 undefined 이다
  - null: 0에 가깝고, type은 object이다

## eqeq(==) 줄이기

javascript에서는 `==` 이 아닌 `===` 을 사용하자

```js
'1' == 1 // true
'1' === 1 // false
```

## 형변환 주의하기

```js
// ❌ 암묵적
11 + ' 문자와 결합' // '11 문자와 결합'
!!'문자열' // true
!!'' // false

// ✅ 명시적
// parseInt를 사용할 때 진수 표현을 넣는 것이 좋다
parseInt('9.9999', 10); // 10

String(11 + ' 문자와 결합')
Boolean('문자열') // true
Boolean('') // false
```

## isNaN

- 10진수 -> 사람
- 2진수 -> 컴퓨터

여기서 소수점을 표현할 때 간극이 발생하는데
javascript에서 부동소수점을 표현할 때, [IEEE 754](https://ko.wikipedia.org/wiki/IEEE_754)를 사용한다

```js
Number.MAX_SAFE_INTEGER // 9007199254740991
Number.isInteger // ƒ isInteger() { [native code] }

 // isNaN은 값이 뒤집어져 귀결되므로 헷갈릴 수 있다
isNaN(123) // false // 숫자가 숫자가 아니다

isNaN(123 + '테스트') // true
Number.isNaN(123 + '테스트') // false // '123테스트'는 string이기 때문에 NaN이 아니다

isNaN // 느슨한 검사
Number.isNaN // 엄격한 검사
```

- isNaN: isNaN 함수는 인자를 숫자로 변환할 수 있는지 여부를 검사한다. 인자가 숫자로 변환될 수 없다면 true를, 변환될 수 있다면 false를 반환한다.
- Number.isNaN: 인자로 들어온 값이 NaN이어야만 참(true)을 리턴한다.
