# array

## Javascript의 배열은 `객체`다

```js
const arr = [1,2,3]

arr[3] = 'test'
arr['property'] = 'string value'
arr['obj'] = {}
arr[{}] = [1,2,3]
arr['func'] = function () {
  return 'hello'
}

for (let i = 0; i < arr.length; i++) {
  console.log(arr[i])
}
/**
 * 출력
 * 1
 * 2
 * 3
 * test
 * ❗️ for문의 let이 Number이기 때문에 출력이 안된다
 */

// 실제 arr 값
console.log(arr)
/**
[
  1,
  2,
  3,
  'test',
  property: 'string value',
  obj: {},
  '[object object]': [1,2,3],
  func: ƒ
]
*/
```

- 배열을 아래와 같이 생각해 볼 수 있기 때문에 배열을 다룰 때는 주의를 해야한다

```js
const arr = [1,2,3]

const obj = {
  0: 1,
  1: 2,
  2: 3
}
```

- javascript에서 배열을 확인할 때는 `Array.isArray()`를 사용하자

## Array.length

array의 length를 다룰 때는 주의해야 한다.

```js
const arr = [1,2,3]
console.log(arr.length) // 3
arr.length = 10
console.log(arr.length) // 10
console.log(arr) // ❗️ [1,2,3,,,,,,,,]
```

```js
const arr = [1,2,3]
arr[3] = 4
console.log(arr.length) 3
arr[9] = 10
console.log(arr) // ❗️ [1,2,3,,,,,,,,10]
```

이런 array의 성질을 역이용할 수 있다

```js
Array.prototype.clear = function () {
  this.length = 0
}

function clearArray(array) {
  array.length = 0

  return array
}

const arr = [1,2,3]
console.log(arr.clear()) // []
console.log(clearArray(arr)) // []
```

## 배열 요소에 접근하기

### 첫 번째 케이스

```js
function operateTime(inputs, operators, is) {
  inputs[0].split('').forEach((num) => {
    cy.get('.digit').contains(num).click()
  })

  inputs[1].split('').forEach((num) => {
    cy.get('.digit').contains(num).click()
  })
}
```

```js
function operateTime(inputs, operators, is) {
  const [firstInput, secondInput] = inputs
  firstInput.split('').forEach((num) => {
    cy.get('.digit').contains(num).click()
  })

  secondInput.split('').forEach((num) => {
    cy.get('.digit').contains(num).click()
  })
}
```

```js
function operateTime([firstInput, secondInput], operators, is) {
  firstInput.split('').forEach((num) => {
    cy.get('.digit').contains(num).click()
  })

  secondInput.split('').forEach((num) => {
    cy.get('.digit').contains(num).click()
  })
}
```

### 두 번째 케이스

```js
function clickGroupButton() {
  const confirmButton = document.getElementsByTagName('button')[0]
  const cancelButton = document.getElementsByTagName('button')[0]
  const resetButton = document.getElementsByTagName('button')[0]

  ...
}
```

```js
function clickGroupButton() {
  const [confirmButton,cancelButton,resetButton] = document.getElementsByTagName('button')

  ...
}
```

### 세 번째 케이스

```js
function formatDate(targetDate) {
  const date = targetDate.toISOString().split('T')[0]
  const [year, month, day] = date.split('-')

  return `${year}년 ${month}월 ${day}일`
}
```

```js
function formatDate(targetDate) {
  const [date] = targetDate.toISOString().split('T')
  const [year, month, day] = date.split('-')

  return `${year}년 ${month}월 ${day}일`
}
```

### 유틸 함수 만들기

(e.g. lodash의 `_.head`)

```js
function head(arr) {
  return arr[0] ?? ''
}

function formatDate(targetDate) {
  const date = head(targetDate.toISOString().split('T'))
  const [year, month, day] = date.split('-')

  return `${year}년 ${month}월 ${day}일`
}
```

### 유사 배열 객체

```js
const arrayLikeObject = {
  0: 'HELLO',
  1: 'WORLD',
  length: 2
}

const arr = Array.from(arrayLikeObject)

console.log(Array.isArray(arrayLikeObject)) // false
console.log(Array.isArray(arr)) // true

console.log(arr) // ['HELLO','WORLD']
```

- arguments

```js
function generatePriceList() {
  return arguments.map((arg) => arg + '원') // arguments는 유사 배열 객체
}

generatePriceList(100, 200, 300, 400, 500, 600)
```

- for문으로 돌긴하지만 유사배열이라 고차함수를 쓸 수 없다
- 고차함수를 쓰려면 `Array.from`을 사용해 주어야 한다

```js
function generatePriceList() {
  console.log(Array.isArray(arguments)) // false

  for (let idx = 0; idx < arguments.length; index++>) {
      const element = arguments[idx]

    console.log(element) // 100, 200, 300, 400, 500
  }
}

generatePriceList(100, 200, 300, 400, 500, 600)
```

## 불변성 (immutable)

```js
const originArray = ['123', '456', '789']

const newArray = originArray
const copyArray = [...originArray]

originArray.push(10)
originArray.push(11)
originArray.push(12)
originArray.unshift(0)

console.log(newArray) // [0, '123', '456', '789', 10, 11, 12]
console.log(originArray) // [0, '123', '456', '789', 10, 11, 12]
console.log(copyArray) // ['123', '456', '789']
```

- 배열에서 불변성을 지키는 방법
  1. 배열을 복사한다 (얕은 복사 주의)
  2. 새로운 배열을 반환하는 메서드들을 활용한다 (e.g. `filter`, `map`, `slice`)

## for문 배열 고차함수로 리팩터링

```js
const price = ['2000', '1000', '3000', '5000', '4000']

function getWonPrice(priceList) {
  let temp = []

  for (let i = 0; i < priceList.length; i++>) {
    temp.push(priceList[i] + '원')
  }

  return temp
}
```

```js
const price = ['2000', '1000', '3000', '5000', '4000']

function getWonPrice(priceList) {
  return priceList.map((price) => price + '원')
}
```

```js
const price = ['2000', '1000', '3000', '5000', '4000']
const isOverOneThousand = (price) => Number(price) > 1000
const ascendingList = (a, b) => a - b

const suffixWon = (price) => price + '원'

function getWonPrice(priceList) {
  const isOverList = priceList.filter(isOverOneThousand)
  const sortList = isOverList.sort(ascendingList)

  return sortList.map(suffixWon)
}
```

## 배열 메서드 체이닝 활용하기

```js
function getWonPrice(priceList) {
  return priceList
    .filter(isOverOneThousand)
    .sort(ascendingList)
    .map(suffixWon)
}
```

## `map` vs `forEach`

```js
const prices = ['1000','2000','3000']

const newPricesForEach = prices.forEach((price) => price + '원')
const newPricesMap = prices.map((price) => price + '원')

console.log(newPricesForEach) // undefined
console.log(newPricesMap) // ['1000원','2000원','3000원']
```

- forEach: 그저 배열을 순회하며 또 다른 함수를 실행해준다
- map: 배열을 순회하며 또 다른 배열을 생성한다

## Continue & Break

`forEach`, `map`, `filter`, `reduce` 같은 고차 함수들은 배열을 순회 중에 제어하기 어렵다

```js
const orders = ['first','seconde','third']

orders.forEach((order) => { // map, filter, reduce 동일
  if (order === 'second') {
    break;
  }

  console.log(order) // ❌ Error
})

// 대안1: try catch
try {
  orders.forEach((order) => { // map, filter 동일
  if (order === 'second') {
    throw Error
  }

  console.log(order)
})
} catch (e) {
  ...
}

// 대안2: for문
// 대안3: for of
// 대안4: for in

// 다른 대안: every, some, find, findIndex 메서드와 함께 사용
```
