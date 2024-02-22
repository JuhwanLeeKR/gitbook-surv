# object

## Computed Property Name

javascript를 잘 알아야 한다.

```jsx
// 속성도 동적으로 받을 수 있다
const handleChange = (e) => {
  setState({
    [e.target.name]: e.target.value, // [e.target.name] 부분이 Computed Property Name
  })
}
```

```jsx
const noop = createAction('INCREMENT')

const reducer = handleActions(
  {
  [noop]: (state, action) => ({
    counter: state.counter + action.payload
  })
  },
  { counter: 0 }
)
```

## Lookup Table

key와 value 쌍으로 구성된 table이라 생각하면 쉽다.

```js
function getUserType(type) {
  if (type === 'ADMIN') {
    return '관리자'
  } else if {
    return '강사'
  } else if {
    return '수강생'
  } else {
    return '해당 없음'
  }
}
```

```js
function getUserType(type) {
  switch (key) {
    case 'ADMIN':
      return '관리자'
    case 'INSTRUCTOR':
      return '강사'
    case 'STUDENT':
      return '수강생'
    case 'STUDENT2':
      return '수강생'
    default:
      return '해당 없음'
  }
}
```

이렇게 될 때 `Lookup Table`을 사용할 수 있다.

```js
function getUserType(type) {
  const USER_TYPE = {
    ADMIN: '관리자',
    INSTRUCTOR: '강사',
    STUDENT: '수강생',
    UNDEFINED: '해당 없음',
  }

  return USER_TYPE[type] ?? USER_TYPE[UNDEFINED]
}
```

### BEST PRACTICE

```js
function getUserType(type) {
  return (
    {
      ADMIN: '관리자',
      INSTRUCTOR: '강사',
      STUDENT: '수강생',
    }[type] ?? '해당 없음'
  )
}
```

- ✅ Better

```js
import USER_TYPE from './constants/...'

function getUserType(type) {
  return USER_TYPE[type] || USER_TYPE.UNDEFINED
}
```

## 객체 분해 구조 할당 (Object Destructuring)

```js
function Person({name, age, location}) {
  this.name = name
  this.age = age
  this.location = location
}

const juhwan = new Person({
  name: 'juhwan',
  age: 30,
  location: 'korea',
})
```

```js
function Person(name, {age, location}) {
  this.name = name
  this.age = age
  this.location = location
}

const juhwanOption = {
  age: 30,
  location: 'korea'
}

const juhwan = new Person('juhwan', juhwanOption)
/** OR
 const juhwan = new Person('juhwan', {
  age: 30,
  location: 'korea'
 })
 **/
```

```jsx
const orders = ['First','Second','Third']

const st = orders[0] // ❌
const rd = orders[2] // ❌

const [first, , third] = orders // ❌

const {0: st2, 2:rd2} = orders // ✅ 객체도 object로 뽑을 수 있다
```

## 객체를 동결한다 (Object.freeze)

shallow 복사라는 것을 알고 있자

```js
const STATUS = {
  PENDING: 'PENDING',
  SUCCESS: 'SUCCESS',
  FAIL: 'FAIL',
}

const STATUS_FREEZE = Object.freeze({
  PENDING: 'PENDING',
  SUCCESS: 'SUCCESS',
  FAIL: 'FAIL',
})

STATUS_FREEZE.PENDING = 'foo'
console.log(STATUS_FREEZE) //{ PENDING: 'PENDING', SUCCESS: 'SUCCESS', FAIL: 'FAIL' }

STATUS_FREEZE.FOO = 'foo'
console.log(STATUS_FREEZE) //{ PENDING: 'PENDING', SUCCESS: 'SUCCESS', FAIL: 'FAIL' }

Object.isFrozen(STATUS) // true
Object.isFrozen(STATUS.PENDING) // true
Object.isFrozen(STATUS.SUCCESS) // true
```

### Shallow copy vs Deep copy

**`Object.freeze`도 깊은 복사에는 관여하지 못한다**

```js
const STATUS_FREEZE = Object.freeze({
  PENDING: 'PENDING',
  SUCCESS: 'SUCCESS',
  FAIL: 'FAIL',
  OPTIONS: {
    GREEN:'GREEN',
    RED:'RED',
  }
})

Object.isFrozen(STATUS_FREEZE.OPTIONS) // false
```

>해결법
> -1. lodash
> -2. 직접 유틸 함수 생성
> -3. stackoverflow
> -4. typescript

```js
function deepFreeze(targetObj) {
  Object.keys(targetObj).forEach((key) =>{
    if (/* 객체가 맞다면*/)
      deepFreeze(targetObj[key]) // 재귀
    })
}

// 많은 코드들이 있다
```

## Prototype 조작 지양하기

`prototype` 객체를 조작하면 어디서나 사용 가능하니 조작을 지양하자

1. 이미 javascript는 많이 발전했다. (e.g. lodash, 마플)
  1-1. 직접 만들어서 모듈화
  1-2. 직접 만들어서 모듈화 => 배포 => NPM
2. JS 빌트인 객체를 건들지 말자.

```js
// 클래스 사용
class Car {
  constructor(name, brand) {
    this.name = name
    this.brand = brand
  }

  sayName() {
    return this.brand + '-' + this.name
  }
}
```

```js
// 생성자 함수 사용
function Car(name, brand) {
    this.name = name
    this.brand = brand
}

Car.prototype.sayName = () => {
  return this.brand + '-' + this.name
}
```

## hasOwnProperty

```js
const person = {
  name: 'juhwan'
}
person.hasOwnProperty('name') // true
person.hasOwnProperty('foo') // false

for (const key in object) {
  if (Object.hasOwnProperty.call(object, key)) {
    const element = object[key]
  }
}
```

`hasOwnProperty`를 그냥 사용하게 되면 다른 객체에 있는 `hasOwnProperty`를 사용할 수 있기 때문에, `.call()`을 사용한다 (`this`를 변경해야하기 때문)

```js
const foo = {
  hasOwnProperty: function () {
    return 'hasOwnProperty'
  }
  bar: 'string',
}

console.log(foo.hasOwnProperty('bar')) // hasOwnProperty
console.log(Object.prototype.hasOwnProperty.call(foo, 'bar')) // true
```

- 단축하기

```js
function hasOwnProp(targetObj, targetProp) {
  return Object..prototype.hasOwnProperty
    .call(targetObj, targetProp)
}
```

## 직접 접근 지양하기

```js
// ❌
const model = {
  isLogin: false,
  isValidToken: false
}

function login() {
  model.isLogin = true
  model.isValidToken= true
}

function logout() {
  model.isLogin = false
  model.isValidToken= false
}
```

```js
// ❌ 모델에 접근하는 것이 너무 열려있다
const model = {
  isLogin: false,
  isValidToken: false
}

function login() {
  model.isLogin = true
  model.isValidToken= true
}

function logout() {
  model.isLogin = false
  model.isValidToken= false
}
```

```js
// ✅ 객체에 직접 접근하는 것을 따로 만들자
const model = {
  isLogin: false,
  isValidToken: false
}

function setLogin(bool) {
  model.isLogin = bool
}

function setValidToken(bool) {
  model.isValidToken = bool
}

function login() {
  setLogin(true)
  setValidToken(true)
}

function logout() {
  setLogin(false)
  setValidToken(false)
}
```

redux나 vuex같은 `flux 패턴`을 보면 복잡하다
(e.g. flux => action => reducer => state변화)

❓ **예측 가능한 상태 컨테이너를 만들어야 하기 때문에**

`예측 가능한 코드를 작성해서 동작이 예측 가능하게 만드는 것을 지양하자`

javascript object의 `get`, `set`을 사용해보자

## Optional Chaining (?.)

```js
const obj = {
  name: 'value'
}

obj?.name
```

```js
const response = {
  data: {
    userList: [
      {
        name: 'juhwan'.
        info: {
          tel: '010',
          email: 'dev',
        }
      }
    ]
  }
}

response.data.userList[0].info.email // 런타임에서 터질 수 있다

// ❌ 아래 경우에도 문제가 생길 수 있다 (response에 data가 없을 수 있음)
function getUserEmailByIndex(userIndex) {
  if (response.data.userList) {
    return response.data.userList[userIndex].info.email
  }

  return '알 수 없는 에러가 발생했습니다'
}

function getUserEmailByIndex(userIndex) {
  if (response?.userList?.[userIndex]?.info?.email) {
    return response.data.userList[userIndex].info.email
  }

  return '알 수 없는 에러가 발생했습니다'
}
```
