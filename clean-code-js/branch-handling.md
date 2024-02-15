# branch handling

## 값, 식, 문

프로그래밍에서 컴퓨터에게 명령을 내리기 위해 문법을 사용한다. 문법을 정확하게 사용하는 것은 프로그램이 의도대로 작동하게 만드는 데 필수적이다.
프로그래밍 언어는 기본적으로 값(value), 식(expression), 문(statement)으로 구성되며, 각각은 프로그램에서 데이터를 다루고 로직을 구성하는 방식에 중요한 역할을 한다.

- 값(Value): 데이터의 한 조각으로, 문자열 "Hello, World!", 숫자 42 또는 불리언 true와 false와 같이 변경할 수 없는 데이터를 의미한다.
- 식(Expression): 값들을 조합하고 연산하여 새로운 값을 만들어내는 코드 조각. 예를 들어, 5 * 10 또는 name.toUpperCase()과 같은 식을 말한다.
- 문(Statement): 프로그램에서 실행 가능한 최소한의 독립적인 코드 단위로, 어떤 동작을 수행하도록 지시하는 것을 말한다. 변수 선언이나 if 조건문, for 루프 등이 이에 해당한다.

**올바른 위치에 올바른 코드를 넣어야 한다.**

```jsx
// jsx

<div id={if (condition) {'msg'}}>Hello, World!</div> // ❌

// 삼항 연산자 사용
<div id={condition ? 'msgTrue' : 'msgFalse'}>Hello, World!</div> // ✅
// 논리 연산자 사용
<div id={condition && 'msgTrue'}>Hello, World!</div> // ✅
```

## 삼항 연산자

- 과도한 숏코딩(short coding) 보다는 일관성, 가독성이 중요하다.

```txt
조건 ? 참 [값, 식] : 거짓 [값, 식]
```

### switch 문을 활용해보는 것은 어떨까?

```js
// 가독성 낮음
function example() {
  return condition1 ? value1
    : condition2 ? value2
    : condition3 ? value3
    : value4
}

// 가독성이 좀 더 있긴 하지만 switch 문이 더 나음
function example() {
  if (condition1) return value1
  else if (condition2) return value2
  else if (condition3) return value3
  else return value4
}

function example() {
  switch (true) {
    case condition1:
      return value1;
    case condition2:
      return value2;
    case condition3:
      return value3;
    default:
      return value4;
  }
}

function example() {
  // 조건을 평가하여 결과를 const 변수에 할당
  const conditionResult = ...some logic

  switch (conditionResult) {
    case 'value1':
      return value1;
    case 'value2':
      return value2;
    case 'value3':
      return value3;
    case 'value4':
      return value4;
  }
}

```

### 괄호를 사용해 보자

```js
const example = condition1
  ? a === 0
    ? 'zero' : 'positive'
  : 'negative'

const example = condition1
  ? (a === 0 ? 'zero' : 'positive')
  : 'negative'
```

### 반환 값이 없을 때는 삼항 연산자를 사용하지 말자

> ❗️ 개인적인 선호 스타일에 따라 다를 수 있음

```js
// ❌
function alertMessage(isAdult) {
  isAdult
    ? alert('입장이 가능합니다.')
    : alert('입장이 불가능합니다.')
}

// ✅
function alertMessage(isAdult) {
  if (isAdult) {
    alert('입장이 가능합니다.')
  } else {
    alert('입장이 불가능합니다.')
  }
}
```

### 3개의 피연산자가 아닌 경우에는 삼항 연산자가 아닌 ==논리 연산자==를 사용하자

## 단축 평가 (short-circuit evaluation)

```js
/**
 * AND
 **/
true && true && '도달 O' // '도달 O'
true && false && '도달 O' // false

/**
 * OR
 **/
false || false || '도달 O' // '도달 O'
false || true || '도달 O' // true
```

```js
function fetchData() {
  return state.data || 'Fetching...'
}
```

## else if, else 피하기

`else if`를 `Promise then chaining`으로 착각하는 경우가 있는데 **아니라는 것**을 명심하자!

```js
const x = 1

// 두 if 문은 같다
if (x >= 0) {
  'x는 0과 같거나 크다'
} else if (x > 0) {
  'x는 0보다 크다'
} else {
  'Else'
}

if (x >= 0) {
  'x는 0과 같거나 크다'
} else {
  if (x > 0) {
    'x는 0보다 크다'
  }
}
```

```js
function getActiveUserName(user) {
  if (user.name) {
    return user.name
  } else {
    return '이름없음'
  }
}

function getActiveUserName(user) {
  return user.name || '이름없음'
}
```
