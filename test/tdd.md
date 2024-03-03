# tdd

<!--
TDD
- TDD란
- Jest
- Describe - Context - It 패턴
- 단위테스트란
 -->

## TDD (Test Driven Development) 란?

테스트 코드를 먼저 작성하는, 즉 구현보다 인터페이스와 스펙을 먼저 정의함으로써 개발을 진행하는 방식.

### *TDD Cycle*

1. `Red` → 실패하는 테스트 코드를 작성. 인터페이스와 스펙에 집중한다.
2. `Green` → 재빨리 테스트를 통과시킨다. 올바른 방법이 아니어도 괜찮다.
3. `Refactor` → 리팩터링을 통해 코드를 올바르게 만든다. TDD에서 가장 중요한 부분이지만, 간과될 때가 많다.

- 작은 단계를 찾고(시간을 짧게 가져가야 한다), 코드에서 피드백을 얻는 게 (어렵고) 중요하다.
- 2번이 어렵다면 1번으로 돌아가서 더 작고 쉬운 문제를 정의하고, 3번을 위해 의도를 드러내고 중복을 찾아 제거하는 연습을 해야 한다.

이 둘이 익숙하지 않으면 TDD를 하는 게 거의 불가능하고, 사실 이 둘이 어려우면 일반적인 개발 또는 클린 코드를 작성하는 것 또한 매우 힘들다.

## [Jest](https://jestjs.io/)

### 테스트 케이스를 정의하는 두 가지 방법

1. test 함수로 개별 테스트를 나열하는 방식.
2. BDD 스타일로 주체-행위 중심으로 테스트를 조직화하는 방식.

- jest에서 typescript를 사용하기 위한 설정

```js
// jest.config.js
module.exports = {
 testEnvironment: 'jsdom',
 setupFilesAfterEnv: [
  '@testing-library/jest-dom/extend-expect',
 ],
 transform: {
  '^.+\\.(t|j)sx?$': ['@swc/jest', {
   jsc: {
    parser: {
     syntax: 'typescript',
     jsx: true,
     decorators: true,
    },
    transform: {
     react: {
      runtime: 'automatic',
     },
    },
   },
  }],
 },
};
```

```ts
// foo.test.ts foo.spec.ts(BDD 스타일)

function add1(...numbers: number[]): number {
  return (number[0] ?? 0) + (numbers[1] ?? 0)
}

// refactor add1
function add(...numbers: number[]): number {
  if (numbers.length === 0) {
    return 0
  }
  // 1. reduce
  return numbers.reduce((acc, number) => acc + number)

  // 2. 재귀
  return add(...numbers.slice(0, numbers.length - 1))
      + numbers[numbers.length -1]
}

// 한 가지를 테스트할 때,
test('add', () => {
  expect(add(1, 2)).toBe(3)
})

// 다양한 케이스를 테스트할 때,

// 가능하지만 의도가 명확하지 않다
test('add', () => {
  // 인자가 없으면 0
  expect(add()).toBe(0)
  // 인자가 2개면 2개의 합
  expect(add(1, 2)).toBe(3)
  // 인자가 3개면 3개의 합
  expect(add(1, 2, 3)).toBe(6)
})


const context = describe // R spec에서 정의하였으나, jest에서 context를 지원하지 않기 때문에 변수할당

describe('add', () => {
  context('with two arguments', () => {
    it('두 숫자의 합을 리턴한다', () => { // returns sum of two numbers
      expect(add(1, 2)).toBe(3)
    })
  })

  context('with only one argument', () => {
    it('returns the same number', () => {
      expect(add(2)).toBe(2)
    })
  })

  context('with no argument', () => {
    it('returns zero', () => {
      expect(add()).toBe(0)
    })
  })

  context('with ten arguments', () => {
    it('returns sum of ten numbers ', () => {
      expect(add(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)).toBe(55)
    })
  })
})
```

>**참고 링크**
>
>- [테스트 주도 개발 (with. Ashal)](https://github.com/ahastudio/til/blob/main/agile/test-driven-development.md)
>- [TDD FAQ (with. Ashal)](https://github.com/ahastudio/til/blob/main/blog/2016/12-03-tdd-faq.md)
>- [Jest를 이용한 간단한 TDD 예제 (with. Ashal)](https://github.com/ahastudio/til/blob/main/jest/20201204-simple-tdd-example.md)
>- [Given, when, then (with. Ashal)](https://github.com/ahastudio/til/blob/main/blog/2018/12-08-given-when-then.md)
