# React-testing-library

<!--
React-testing-library keyword
- React Testing Library
- given - when - then 패턴
- Mocking
- Test fixture
 -->

## React Testing Library란?

React 컴포넌트를 사용자 입장에 가깝게 테스트할 수 있는 도구

### [Given - when - then 패턴](https://martinfowler.com/bliki/GivenWhenThen.html)

준비 - 실행 - 검증 순으로 테스트 코드를 구분해서 작성하는 패턴

```tsx
// TextField.tsx 컴포넌트가 있다고 가정
// TextField.test.tsx
import { render, screen, fireEvent } from '@testing-library/react'

import TextField from './TextField'

test('TextField', () => {
  // given
  const label = 'Name'
  const text = 'Tester'

  const setText = jest.fn()

  // when
  render((
    <TextField
      label={label}
      placeholder=""
      text={text}
      setText={setText}
    />
  ))

  // then
  screen.getByLabelText(label) // 정규식 사용 가능 (e.g. /Sear/)
  screen.getByDisplayValue(text) // expect(input.value).toBe(text)
  screen.getByPlaceholderText(/name/)

  // ---
  // when
  const input = screen.getByLabelText(label)
  fireEvent.change(input, {
    target: {value: 'New Name'}
  })

  // then
  expect(setText).toBeCalledWith('New Name')
})
```

- context를 사용하는 방향으로 리팩터링

```tsx

const context = describe

describe('TextField', () => {
  // given
  const label = 'Name'
  const text = 'Tester'

  const setText = jest.fn()

  beforeEach(() => { // 매번 초기화 해줌
    jest.clearAllMocks() // setText.mockClear()로 특정 요소를 초기화할 수 있음
  })

  function renderTextField() {
    render((
      <TextField
        label={label}
        placeholder=""
        text={text}
        setText={setText}
      />
    ))
  }

  function inputText(value: string) {
    const input = screen.getByLabelText(label)
    fireEvent.change(input, {
      target: {value}
    })
  }

  it ('renders elements', () => {
    // when
    renderTextField()

    // then
    screen.getByLabelText(label) // 정규식 사용 가능 (e.g. /Sear/)
    screen.getByDisplayValue(text) // expect(input.value).toBe(text)
    screen.getByPlaceholderText(/name/)
  })

  context('when user enters name', () => {
    beforeEach(() => {
      //given
      renderTextField()
    })

    it ('calls "setText" handler', () => {
      // when
      inputText('New Name')

      // then
      expect(setText).toBeCalledWith('New Name')
    })
  })
})
```

## Jest MOCK

```tsx
jest.mock('./foo/bar', () => () => [
  {
    category: 'Fruits', price: '$1', stocked: true, ...
  }
])
```

- 위 방식으로 하면 매번 번거롭기 때문에 fixture를 만들어준다

```tsx
// fixtures/products.ts
export const products = [
  {
    category: 'Fruits', price: '$1', stocked: true, ...
  }
]
```

```tsx
import fixtures from '../fixtures' // 실제로 이렇게 import 시키려면 index.ts 작업(모듈화)이 선행되어야 함

jest.mock('./foo/bar', () => () => fixtures.products)
```

- 아니면 `__mock__` 파일을 생성해서 작업을 할수도 있다.

```ts
// __mocks__/bar.ts
import fixture from '../../fixtures'

const bar = jest.fn(() => fixtures.products)
// const bar = () => fixtures.products

export default bar
```

```tsx
// test 파일
jest.mock('./foo/bar')
```

>**참고 링크**
>
>- [React Testing Library Github](https://github.com/testing-library/react-testing-library)
>- [Jest Dom Github](https://github.com/testing-library/jest-dom)
