# abstract

## Magic Number

적절한 추상화를 통해 Magic number들을 명시적으로 사용할 수 있다

```js
setTimeout(() => {
  scrollToTop()
}, 3 * 60 * 1000) // 세 번의 의식적인 흐름이 들어간다.


// util.ts constants.ts
export const COMMON_DELAY_MS = 3 * 60 * 1000

setTimeout(() => {
  scrollToTop()
}, COMMON_DELAY_MS)

// Numeric Operator
const PRICE = {
  MIN: 1_000_000,
  MAX: 100_000_000,
}

// Min, Max
getRandomPrice(PRICE.MIN, PRICE.MAX)

// ❌ hard coding
function isValidName(name) {
  return carName.length >= 1 && carName.length <= 5
}

// ✅
 // ts
const CAR_NAME_LEN = {
  MIN: 1,
  MAX: 5,
} as const

const CAR_NAME_LEN = Object.freeze({
  MIN: 1,
  MAX: 5,
})

function isValidName(name) {
  return carName.length >= CAR_NAME_LEN && carName.length <= CAR_NAME_LEN.MAX
}

function notiValidName = (value) => {
  if (!isArrayItemLengthRange(names, CAR_NAME_LEN.MIN, CAR_NAME_LEN.MAX)) {
    alert(`!!`)
  }
}

```

## 네이밍 컨벤션

저장소, 폴더, 파일, 함수, 변수, 상수, 깃 브랜치, 커밋 등
프로그래밍 전반적으로 이름을 네이밍을 위한 규칙이나 관습을 만드는 것

팀이나 개인의 차원에 따라 다를 수 있으며 특히 개인적인 견해와 해석에 따라 다를 수 있다.
하지만 기준을 설정할ㄷ때 기본적인 논리와 이유가 있어야 한다.

**가장 중요한 것은 언어의 예약어(키워드)와 겹치면 안된다.**

### 대표적인 케이스

- camelCase
- PascalCase
- kebab-case
- SNAKE_CASE

### 접두사, 접미사

```js
// prefix-*, *-suffix
data-id
data-name
data-value

AppContainer
BoxContainer

ListComponent
ItemComponent

ICar
TCar

AType
BType

등사-* // 함수는 동사로 시작한다.
_ // private
# // private
```

### 연속적인 규칙

```js
for (let i = 0; i < 10; i++) {
  for (let j = 0; j < 10; j++) {
    for (let k = 0; k < 10; ik++) {
      // ...
    }
  }
}

function func<T, U, V>(name: T, value: U)
```

### 자료형 표현

```js
const inputNumber = 10
const someArr = []
const strToNum = 'some code'
```

### 이벤트 표현

```js
function on-*
function handle-*
function *-Action
function *-Event
function take-*
function *-Query
function *-All
```

### CRUD

```js
function generator-*
function gen-*
function make-*
function get
function set
function remove
function create
function delete
```

### Flag

```js
const isSubmit
const isDisabled
const isString
const isNumber
```

### ETC

```js
function selectBy-* ()
function selectAll
```

## DOM API 접근 추상화

```js
// ❌
export const loader = () => {
  const el = document.createElement('div')
  el.setAttribute('class', 'loading d-flex justify-center mt-3')

  const el2 = document.createElement('div')
  el2.setAttribute('class', 'relative spinner-container')

  const el3 = document.createElement('div')
  el3.setAttribute('class', 'material spinner')

  el.append(el2)
  el2.append(el3)

  return el
}

// ✅
const createLoader = () => {
  const el = document.createElement('div')
  const el2 = document.createElement('div')
  const el3 = document.createElement('div')

  return {
    el, el2, el3
  }
}

const createLoaderStyle = ({el, el2, el3}) => {
  el.setAttribute('class', 'loading d-flex justify-center mt-3')
  el2.setAttribute('class', 'relative spinner-container')
  el3.setAttribute('class', 'material spinner')

  return {
    newEl: el,
    newEl2: el2,
    newEl3: el3
  }
}

export const loader = () => {
  const {el, el2, el3} = createLoader()
  const { newEl, newEl2, newEl3} = createLoaderStyle({el, el2, el3})

  newEl.append(newEl2)
  newEl2.append(newEl3)

  return newEl
}
```
