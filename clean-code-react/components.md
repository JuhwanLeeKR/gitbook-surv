# components

## Self-Closing Tags

- 명시적으로 닫는 태그가 필요 없음

- 기본 HTML 요소인지 아닌지 명확한 차이를 가져야한다.

## Fragment

- Fragment는 DOM에 별도의 노드를 추가하지 않고 여러 자식을 그룹화할 수 있다
- 굳이 사용할 필요가 없을 때는 사용하지 않는 것이 좋다.

```jsx
const Comp = () => {
  return 'string'
}

const Comp = () => {
  return ['arr', 'arr2']
}

const Comp = () => {
  return code
}
```

## 알아두면 좋은 컴포넌트 네이밍

- 일반적으로 컴포넌트는 PascalCase
- 기본 HTML 요소는 lower case
- route based file name (kebab-case)
  - component-naming.jsx => `<ComponentNaming />`
  - component-naming/index.jsx => `<ComponentNaming />`

```jsx
const Comp = () => {
  return (
    <>
      <h1></h1>
      <h2></h2>
      <div></div>
      <input />
      <MyComponent></MyComponent>
      <my-component></my-component>
    </>
  )
}
```

## JSX 컴포넌트 함수로 반환

- 명확한 trade-off가 존재하기 때문에 특별한 이유가 없으면 사용하면 안된다.

```jsx
const ReturnJSXFunction = () => {
  const getComponents =() => {
    return <div>hi</div>
  }

  return (
    <div>
      {getComponents()}
    </div>
  )
}
```

함수로 return 하는 경우 다음과 같은 단점이 있을 수 있다.

1. scope를 알아보기 어렵다.
2. 반환 값을 바로 알기 어렵다.
3. props 전달 등 일반적인 패턴이 아니다.

## 컴포넌트 내부의 inner 컴포넌트 선언

1. 결합도가 증가한다.
   - 구조적으로 스코프적으로 종속돈 개발이 됩니다.
   - 나중에 확장성이 생겨서 분리될때 굉장히 힘들어진다.
2. 성능 저하
   - 상위 컴포넌트 리렌더? => 하위 컴포넌트 재생성

```jsx
const OuterComp = () => { // ❌
  const InnerComponent =() => {
    return <div>INner component</div>
  }

  return (
    <div>
      <InnerComponent>
    </div>
  )
}
```

```jsx
const InnerComponent =() => {
  return <div>INner component</div>
}

const OuterComp = () => { // ✅
  return (
    <div>
      <InnerComponent>
    </div>
  )
}
```

## displayName

- devTool을 사용할 때 displayName을 지정하지 않으면 디버깅이 힘들 수 있다.

1. forwardRef의 사용
2. HOC 패턴의 사용

## 컴포넌트 구성하기

1. 상수는 어디에 선언하나요?
2. 타입 선언 시 interface와 type 중 어떤 걸 사용하나요?
3. 컴포넌트 props 타입명은 어떤 규칙으로 정의하나요?
4. 컴포넌트 선언 시 const와 function 중 어떤 걸 사용하나요?
5. 어떤 순서로 컴포넌트 내부 변수를 선언하나요?
6. useEffect는 어디에 선언하나요?
7. JSX return 하는 규칙이 있나요?
8. Style component는 어디에 선언 하나요?

-> 정답은 없고, 팀의 규칙이나 개인화된 규칙을 따르면 된다.
