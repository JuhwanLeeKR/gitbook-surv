# props

## 불필요한 Props 복사 및 연산

```jsx
const CopyProps = ({value}) => { // ❌
  const [copyValue] = useState(value)

  return <div>{copyValue}</div>
}
```

- 하위 컴포넌트에서 값을 조작하는 경우

```jsx
const CopyProps = ({value}) => { // ❓ 쓸 수는 있지만 합리적이진 않다.
  const [copyValue] = useState(값비싸고_무거운_연산(value))

  return <div>{copyValue}</div>
}
```

- 그냥 값에 넣는다

```jsx
const CopyProps = ({value}) => { // ❓ 그러나 컴포넌트가 렌더링될 때마다 연산이 일어난다.
  const copyValue = 값비싸고_무거운_연산(value)

  return <div>{copyValue}</div>
}
```

- 값 비싸고 무거운 연산이 있다면, 그냥 `useMemo`를 사용한다

```jsx
const CopyProps = ({value}) => { // ✅
  const copyValue = useMemo(() => 값비싸고_무거운_연산(value), [value])

  return <div>{copyValue}</div>
}
```

- props를 복사하는 행위를 지양하자!

## Curly Braces (중괄호)

- 문자열일 경우 중괄호를 생략하는 것이 좋다.

## Shorthand Props

```jsx
const ShorthandProps = ({ isDarkMode, isLogin, ...props}) => {
  return (
    <header
      className="header"
      title="react"
      isDarkMode={isDarkMode}
      isLogin={isLogin}
      hasPadding
      isFixed
      isAdmin
    >
      <ChildComponent {...props} />
    </header>)
}
```

## Single Quotes vs Double Quotes

1. 팀에서 일관적인 규칙만 있으면 된다.
2. HTML? Javascript?
3. Prettier(포매팅 도구), ESLint 속성만 잘 따르면 된다.

## 알아두면 좋은 Props 네이밍

```jsx
const PropsNaming = () => {
  return (
    <ChildComponent // ❌
      class="header" // className
      Title="react" // title
      is_dark_mode={isDarkMode} // isDarkMode
      isLogin={isLogin}
      otherComponent={OtherComponent} // OtherComponent
      isFixed
    />
  )
}
```

## 인라인 스타일 주의하기

JSX에서 인라인 스타일을 쓰려면 중괄호 안에 camelCase key를 가진 객체를 넣어야 한다

## CSS in JS 인라인 스타일 지양하기

1. 성능 저하를 일으킴
2. 휴먼 에러가 발생할 수 있음
3. export 할 수 없음

## 객체 Props 지양하기

- Object가 육안으로 같은 값으로 보여도 javascript 상에서는 다른 값으로 인식한다.

```js
  Object.is(['hi'],['hi']) // false
  Object.is({ hello: "world"},{ hello: "world"}) // false
```

```jsx
const SomeComp = () => {
  return (
    <ChildComponent // ❌ 불필요한 리렌더링이 일어날 수 있다
      propObj={{ hello: "world"}}
      propArr={[ "hello", "hello"]}
    />
  )
}
```

- 변하지 않는 값일 경우 컴포넌트 외부로 드러내기
- 필요한 값만 객체를 분해해서 Props로 내려준다.
- 컴포넌트를 더 평탄하게 나누면 나눌 Props 또한 평탄하게 나눠서 내릴 수 있다.

```jsx
const SomeComp = ({heavyState}) => {
  const [propArr, setPropArr] = useState(["hello", "hello"])

  // 너무 무겁거나 자주 사용되는 값인 경우에만 useMemo를 사용한다
  const computedState = useMemo((() => ({
    heavyState: heavyState
  })), [heavyState])

  return (
    <ChildComponent //
      hello='world'
      hello2={propsArr.at(0)}
      computedState={computedState}
    />
  )
}
```

## HTML Attribute 주의하기

HTML, JS에서 정의한 예약어와 커스텀 컴포넌트 props가 혼용되지 않도록 하자 (e.g. button type)

## ...props 주의할 점

- 코드를 예측하기 어렵다

```jsx
const ParentComponent = (props) => {
  return <ChildrenHOCComponent {...props} />
}
```

- props에서 spread 연산자가 쓰이면 `관련 있는 props`, `없는 props`, `나머지 props`로 나눠보자

## 많은 Props 일단 분리하기

너무 많은 Props를 넘기는 경우 => 결과보다는 일단 실행 => 분리의 대상?

=> TanStack Query, Form Library, 상태 관리자, Context API, Composition

```jsx
const App = () => { // ❌
  return (
    <JoinForm
      user={user}
      auth={auth}
      location={location}
      favorite={favorite}
      handleSubmit={handleSubmit}
      handleReset={handleReset}
      handleCancel={handleCancel}
    />
  )
}
```

```jsx
const App = () => { // ✅
  // Step1. One Depth 분리를 한다.
  // Step2. 확장성을 위한 분리를 위해 도메인 로직을 다른 곳으로 모아넣는다.

  return (
    <JoinForm
      onSubmit={handleSubmit}
      onReset={handleReset}
      onCancel={handleCancel}
    >
      <CheckBoxForm formData={user}/>
      <CheckBoxForm formData={auth}/>
      <RadioButtonForm formData={location}/>
      <SectionForm formData={favorite}/>
    </JoinForm>
  )
}
```

- Props가 많다면 컴포넌트를 분리해보자.

## 객체보다는 단순한 Props의 장점

언젠간 쓸 것 같아서 전체 객체를 내리는 것보다는 객체를 구조 분해 할당해서 내리는 것이 더 좋다.
