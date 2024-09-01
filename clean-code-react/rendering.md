# rendering

## JSX에서의 공백처리

`&nbsp;` 보다는 `{' '}`

## 0(Zero)는 JSX에서 유효한 값

- 0은 jsx에서 유효하기 떄문에 렌더링 된다.
- [Conditional rendering](https://react.dev/learn/conditional-rendering)

## 리스트 내부에서의 Key

순회 시 key를 넣을 때 단순 index를 넣거나 렌더링마다 항상 새로운 값을 넣는 것을 경계하자

## 안전하게 Raw HTML 다루기

- HTML Sanitizer API,
- DOMPurify
- eslint-plugin-risxx
