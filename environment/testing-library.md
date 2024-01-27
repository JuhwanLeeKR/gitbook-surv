# testing-library.md

## [**Jest 공식문서**](https://jestjs.io/)

거의 모든 것을 갖춘 테스팅 도구

`Mocha`와 `Chai`처럼 RSpec의 describe-it을 지원하고, expect로 단언(assertion)할 수 있다.
Mocking도 다양한 레벨에서 쉽게 사용할 수 있다.

> **RSpec** 이란?
>
> RSpec은 Ruby 코드를 테스트하기 위해 프로그래밍 언어인 Ruby로 작성된 컴퓨터 도메인별 언어 테스트 도구

- [BETTER SPECS](https://www.betterspecs.org/) (RSpec Best Practice 모음)
- [Ginkgo - Go 언어 개발자를 위한 BDD 테스팅 프레임워크](https://youtu.be/gfTsSBRvdqI) (Go 언어 사례)
- [JUnit5로 계층 구조의 테스트 코드 작성하기](https://johngrib.github.io/wiki/junit5-nested/) (Java 언어 사례 by 기계인간)
- [Let’s RSpec](https://github.com/ahastudio/til/blob/main/ruby/20161206-rspec-let.md) (Jest는 RSpec의 let 같은 걸 지원하지 않기 때문에, 핵심 아이디어를 가져와서 적당한 수준에서 잘 써야 한다.)

## 테스트코드 작성 예시

### 기본적인 테스트 코드

```ts
function add(x: number, y: number): number {
 return (x * 10 + y * 10) / 10;
}

test('add 함수 returns sum of two numbers', () => {
 expect(add(1, 2)).toBe(3);
});
```

### BDD (Behavior Driven Development) 스타일의 테스트 코드

표현력이 좋아지고, 좀 더 고민할 기회를 제공.

```tsx
function add(x: number, y: number): number {
 return (x * 10 + y * 10) / 10;
}

const context = describe;

describe('add 함수는', () => {
 it('returns sum of two numbers', () => {
  expect(add(1, 2)).toBe(3);
 });

 it('returns number', () => {
  expect(typeof add(1, 2)).toBe('number');
 });

 context('두 개의 양수가 주어졌을 때', () => {
  it('항상 두 개의 숫자보다 큰 값을 돌려준다', () => {
   expect(add(1, 2)).toBeGreaterThan(1);
   expect(add(1, 2)).toBeGreaterThan(2);
  });
 });

 context('하나의 양수와 음수가 주어지면', () => {
  it('항상 하나의 양수보다 작은 값을 돌려준다', () => {
   expect(add(1, -2)).toBeLessThan(1);
  });
 });

 context('0.1과 0.2가 주어져도', () => {
  it('이상한 값을 돌려주지 않는다', () => {
   expect(add(0.1, 0.2)).toBe(0.3);
  });
 });
});
```

## React Testing Library

- [**React Testing Library 공식문서**](https://testing-library.com/docs/react-testing-library/intro)
- [**jest-dom**](https://testing-library.com/docs/ecosystem-jest-dom/)

UI 테스트에 특화된 라이브러리. 거의 E2E Test처럼 쓸 수 있다.
단, **"F/E 테스트 = only React 컴포넌트 테스트"가 되는 상황은 최대한 피하는 게 좋다.**
본질에 집중하지 못하고 너무 많은 테스트 코드를 작성할 위험이 있다.
유지보수를 돕기 위해 테스트 코드를 작성하는데, 테스트 코드를 잘못 작성하면 오히려 유지보수를 저해할 수 있다.

### 참고 영상

- [프론트엔드(Front-end)도 테스트해야 하나요?](https://youtu.be/-kUmsKRmOnA)
- [Mocking 때문에 테스트 코드를 작성하기 어렵나요](https://youtu.be/RoQtNLl-Wko)

### 간단한 테스트 코드

```tsx
// Greeting.tsx
type GreetingProps = {
 name: string;
};

export default function Greeting({name}: GreetingProps) {
 return <p>Hello, {name}!</p>;
}
```

```tsx
// Greeting.test.tsx
import {render, screen} from '@testing-library/react';
import Greeting from './Greeting';

describe('Greeting', () => {
 it('renders a greeting message', () => {
  const {getByText} = render(<Greeting name='juhwan' />);
  expect(getByText('Hello, juhwan!')).toBeInTheDocument();
 });

 it('renders a greeting message', () => {
  render(<Greeting name='juhwan' />);
  screen.getByText('Hello, juhwan!');
 });

 it('renders a greeting message', () => {
  render(<Greeting name='juhwan' />);
  expect(screen.queryByText(/Hello/)).toBeInTheDocument();
 });

 it('renders not a greeting message', () => {
  render(<Greeting name='juhwan' />);
  expect(screen.queryByText(/Hi/)).not.toBeInTheDocument();
 });
});

```
