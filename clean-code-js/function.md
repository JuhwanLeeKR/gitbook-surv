# function

## 함수, 메서드, 생성자

함수는 1급 객체로 동작을 하다보니깐 고차함수로 사용할 수 있고, 함수형 프로그래밍도 어느정도 할 수 있다.

- 1급 객체
  - 변수나, 데이터에 담길 수 있다
  - 매개변수로 전달 가능 (콜백 함수)
  - 함수가 함수를 반환 (고차 함수)

```js
// 함수
function func() {
  return this; // global을 바라본다
}

// 객체의 메서드
const obj = {
  method() { // conciseMethod
    return this; // 속한 객체를 바라본다
  }
  conciseMethod: function () {
    return this;
  }
}

// 매서드 => 객체에 의존성이 있는 함수, OOP 행동을 의미
obj.method();

[].map();
'str'.split();

// 생성자 함수 (Class)
function Func() {
  return this // 생성될 인스턴스를 가르킨다
}

// synthetic sugar
class Func {
  constructor() {

  }
}
```

## argument & parameter

```js
function example(parameter) {
  console.log (parameter)
}

const argument = 'foo'

example(argument)
```

- Function parameters are the names listed in the function's definition.
- Function arguments are the real values passed to the function.

- Parameter (Formal Parameter)
- Argument (Actual Parameter)

> [MDN parameters](https://developer.mozilla.org/en-US/docs/Glossary/Parameter)

## 복잡한 인자 관리하기

```js
function toggleDisplay(isToggle) {
  // ...some code
}

function sum(sum1, sum2) {
  // ...some code
}
sum(1, 2)

function genRandomNumber(min, max) {
  // ...some code
}

function timer(start, stop, end) {
  // ...some code
}

function genSquare(top, right, bottom, left) {
  // ...some code
}

// ❌ bad practice
function createCar(name, brand, color, type) {
  return {
    name,
    brand,
    color,
    type,
  }
}

// ✅ refactor
function createCar(name, { brand, color, type}) {
  return {
    name,
    brand,
    color,
    type,
  }
}

createCard('차량 이름', {
  type: 'type'
})

// throw error
function createCar2({name, brand, color, type}) {
  if (!name) {
    throw new Error('name is a required')
  }
  if (!brand) {
    throw new Error('brand is a required')
  }
  return {
    name,
    brand,
    color,
    type,
  }
}
```

## Default Value

```js
// ❌ legacy
function createCarousel(options) {
  options = option || {};
  var margin = options.margin || 0;
  var center = options.center || false;
  var navElement = options.navElement || 'div';

  // ..some code
  return {
    margin,
    center,
    navElement
  }
}

// ✅ Newer
const required = (argName) => {
  throw new Error('required is ' + argName)
}

function createCarousel({
  margin = required('margin'),
  center = false,
  navElement = 'div'} = {}) {
  // ..some code
  return {
    margin,
    center,
    navElement
  }
}
```

## Rest Parameters

```js
// ❌ 추가적으로 인자를 받고 싶은 경우 어려워진다
function sumTotal() {
  Array.isArray(arguments) // false

  return Array.from(arguments).reduce(
    (acc, cur) => acc + cur
  )
}

// ✅ Array.from을 쓰지 않아도 되고, 추가적인 변수도 넣을 수 있다
function sumTotal(initValue, ...args){
  Array.isArray(args) // true

  return args.reduce(
    (acc, cur) => acc + cur, initValue
  )
}

```

## void & return

내가 사용하는 API들이 return이 있는지 없는지 정확히 알아보며 사용해야 한다.
(e.g. Array.prototype.push.etc)

```js
// ❌ 기본적으로 아래와 같은 코드를 줄여나가야 한다
// react의 setState나 alert는 void 함수이다
function handleClick() {
  return setState(false)
}
function showAlert(message) {
  return alert(message)
}

// ✅
function handleClick() {
  if (...) {
    setState(false)
    return
  }
  ...
}
function showAlert(message) {
  alert(message)
}

// ❌ 불필요한 return이 있으면 안되는 이유
function test(sum1, sum2) {
  const result = sum1 + sum2
}

function testVoidFunc() {
  return test(1, 2) // undefined
}

// ✅ 반환이 있을 것 같은 네이밍을 활용
function isAdult(age) {
  return age > 19
}

function getUserName(name) {
  return `유저 ${name}`
}
```

> [MDN void](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/void)

## 화살표 함수

화살표 함수를 무조건 사용할 일도, 사용하지 않을 일도 없다
this에 유의한다.

```js
const user = {
  name: 'Juhwan',
  // 상위 scope를 따름. this = global
  getName: () => {
    return this.name;
  }
  newFriends: () => {
    // call, apply, bind 도 사용 불가능
    const newFriendList = Array.from(arguments) // arguments를 사용할 수 없음, rest parameter를 사용해야함
  }

  return this.name + newFriendList
}

user.getName() // undefined

// 화살표로 만든 함수는 생성자로 사용할 수 없음
// 현재 class를 사용하면 되기 때문에 굳이 화살표 함수로 생성자 함수를 만들 필요는 없음
const Person = (name, city) => {
  this.name = name;
  this.city = city;
}

const person = new Person('juhwan', 'korea') // ❌ Error

// class를 다룰 때,
class Parent {
  parentMethod() {
    console.log('parentMethod')
  }

  parentMethodArrow = () => {
    console.log('parentMethodArrow')
  }

  overrideMethod = () => P
  return 'Parent'
}

class Child extends Parent {
  childMethod() {
    super.parentMethod()
  }

  overrideMethod() {
    return 'Child'
  }
}

new Child().childMethod()
new Child().parentMethodArrow() // Error
new Child().overrideMethod() // Parent, 부모의 method가 호출된다

// redux saga, iterator

function* gen() {
  yield () => ?? // ❌ 문법적 지원되지 않음
  yield function name(params) { // ✅
    // ...
  }
}
```

## Callback Function

콜백 함수는 함수를 다른 함수로 넘겨서 제어권을 넘길 수 있다

```js
someElement.addEventListener('click', function() { // 이 함수는 제어권이 개발자가 아닌 사용자에게 넘어간 것이다.
  console.log(someElement + '이 클릭이 되었습니다.')
})

DOM.prototype.addEventListener = function (
  eventType,
  cbFunc
) {
  if (eventType === 'click') {
    const clickEventObject = {
      target: {}
    }
  }

  cbFunc(clickEventObject)
}
```

```js
function register() {
  const isConfirm = confirm(
    '회원가입에 성공했습니다.'
  )

  if (isConfirm) {
    redirectUserInfoPage()
  }
}

function login() {
  const isConfirm = confirm(
    '로그인에 성공했습니다.'
  )

  if (isConfirm) {
    redirectIndexPage()
  }
}

// ✅ Refactoring
function confirmModal(message, cbFunc) {
  const isConfirm = confirm(message)

  if (isConfirm && cbFunc) {
    cbFunc()
  }
}

function register() {
  confirmModal('회원가입에 성공했습니다.', redirectUserInfoPage)
}
function login() {
  confirmModal('로그인에 성공했습니다.', redirectIndexPage)
}
```

## 순수 함수

### Redux

- 예측 가능한 상태 컨테이너
- 순수 함수를 사용해야 한다. (함수에서 사이드 이펙트를 일으키면 안된다)

### Pure function

항상 순수함수를 만든다고 생각하고 작성하는 습관을 들이자

```js
let num1 = 10
let num2 = 20

function impureSum1() {
  return num1 + num2
}

function impureSum2(newNum) {
  return num1 + newNum
}

function pureSum(num1, num2) {
  return num1 + num2
}

// ❌
const obj = {one: 1}
function changeObj(targetObj) {
  targetObj.one = 100

  return targetObj
}
changeObj(obj)
obj // 객체는 primitive 타입과 다르다

// ✅ 객체, 배열 => 새롭게 만들어서 반환
function changeObjPure(targetObj) {
  return {...targetObj, one: 100}
}
```

## Closure

```js
function add(num1) {
  return function sum(num2) {
    return num1 + num2
  }
}



const addOne = add(1)(3)
const addTwo = add(2)(1)
const addThree = add(3)

addThree(1)
```

```js
function add(num1) {
  return function (num2) {
    return function (calculateFn) {
      return calculateFn(num1, num2)
    }
  }
}

function sum(num1, num2) {
  return num1 + num2
}

function multiple(num1, num2) {
  return num1 * num2
}

const addOne = add(5)(2)
const sumAdd = addOne(sum) // 7
const sumMultiple = addOne(multiple) // 10
```

```js
function log(value) {
  return function (fn) {
    fn(value)
  }
}

const logFoo = log('foo')
logFoo((v) => console.log(v));
logFoo((v) => console.info(v));
logFoo((v) => console.error(v));
logFoo((v) => console.warn(v));
```

```js
const arr = [1, 2, 3, 'A', 'B', 'C']

const isNumber = (value) => typeof value === 'number'
const isString = (value) => typeof value === 'string'


// ❌ 클로저를 사용하지 않은 예
function isTypeOf(type, value) {
  return typeof value === type
}

const isNumber = (value) => isTypeOf('number',value)
const isNumber = (value) => isTypeOf('string',value)

// ✅ 클로저를 사용한 예
function isTypeOf(type) {
  return function (value) {
    return typeof value === type
  }
}

const isNumber = (value) => isTypeOf('number')
const isNumber = (value) => isTypeOf('string')
 ```

```js
function fetcher(endpoint) {
  return function (url, options) {
    return fetch(endpoint + url, options)
      .then((res) => {
        if (res.ok) {
          return res.json()
        } else P
        throw new Error(res.error)
      })
      .catch((err) => console.error(err))
  }
}

const naverApi = fetcher('http://naver.com/')
const daumApi = fetcher('http://daum.net/')

naverApi('/webtoon').then((res) => res)
daumApi('/webtoon').then((res) => res)
```

```js
someElement.addEventListener(
  'click',
  debounce(handleClick, 500)
)
someElement.addEventListener(
  'click',
  someFunction
)
someElement.addEventListener(
  'click',
  (e) => {}
)
```
