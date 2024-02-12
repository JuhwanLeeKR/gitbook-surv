# boundary-value

## min - max

1. 최소값과 최대값을 다룬다
2. 최소값과 최대값 포함 여부를 결정해야 한다 (이상-초과 / 이하-미만)
3. 혹은 네이밍에 최소값과 최대값 포함 여부를 표현한다

```js
const MIN_NUMBER = 1;
const MAX_NUMBER = 45;

genRandomNumber(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min
}

const MAX_AGE = 20
function isAdult(age) {
  // 최소값, 최대값 (포함되는지 vs 안되는지)
  // 이상, 초과 vs 이하, 미만
  // 팀 마다 컨벤션이 필요함
  if (age >= 20) {

  }
}

genRandomNumber(MIN_NUMBER, MAX_NUMBER)
isAdult(MAX_AGE)

// 헷갈리기 때문에 아래와 같이 쓸 수도 있으나 이것 또한 헷갈릴 수 있음에 유의
const MIN_IN_NUMBER = 1;
const MIN_NUMBER_LIMIT = 1;
```

## begin - end

체크인 (begin) - 체크아웃 (end)

```js
function reservationDate(beginDate, endDate) {
  ...
}
reservationDate('YYYY-MM-DD','YYYY-MM-DD')
```

## first - last

```js
const STUDENTS = ['A', 'B', 'C']
function getStudents(first, last) {
  ...
}

getStudents('A','C')
```

## prefix - suffix (접두사 - 접미사)

### Prefix

- React Hook: use 접두사는 React 함수형 컴포넌트에서 훅을 사용할 때 널리 사용된다.
  예를 들어, useState, useEffect, useContext 등은 상태 관리, 사이드 이펙트 처리, 컨텍스트 사용을 위한 표준 hook이다.
- Private Properties or Methods: 언어나 프레임워크에서 접근 제한자를 지원하지 않을 때, _(언더스코어) 접두사를 사용하여 프라이빗 속성이나 메서드임을 나타내기도 한다. 예:_privateMethod 또는 _privateVar

### Suffix

- Redux Related Files: Redux를 사용하는 프로젝트에서는 액션(action), 리듀서(reducer), 미들웨어(middleware) 파일명에 접미사를 사용한다.
    예를 들어, userReducer.js, fetchDataMiddleware.js 등이 있다.
- Data Types in C# or Java: C#이나 Java와 같은 언어에서는 변수나 메서드 반환 타입을 명확히 하기 위해 접미사를 사용하기도 한다.
  예를 들어, intCount, nameString, isAvailableBool 등은 타입을 명시합한다.

## **매개변수 순서만 잘 지켜도 경계를 알 수 있다**

- 호출하는 함수의 네이밍과 인자의 순서의 연관성을 고려한다.

1. 매개변수를 2개가 넘지 않도록 만든다.
2. arguments, rest parameter
3. 매개변수를 객체에 담아서 넘긴다.
4. 래핑하는 함수

```js
// (1)
function someFunc1(someArg1, someArg2) {
  ...
}
// e.g.
genRandomNumber(1, 50)
getDates('2024-01-01', '2024-01-31')

// (2)
// ES2015+
function someFunc2(someArg1, ...others) {
  ...
}

// (3)
function someFunc3({someArg1, someArg2, someArg3, someArg4}) {
  ...
}

// (4) 함수가 이미 너무 많이 쓰이는 경우
function someFunc4(someArg1, someArg2, someArg3, someArg4) {
  ...
}

function getFunc4(someArg1, someArg3) {
  someFunc4(someArg1, undefined, someArg3)
}

```
