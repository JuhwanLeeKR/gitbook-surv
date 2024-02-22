# hook

<!--

- React Hook 이란
- Hooks
  - useState
  - useEffect
  - useContext
  - useRef
  - useLayoutEffect
- React StrictMode 란

- useRef
- Hook의 규칙

5.
- usehooks-ts
  - useBoolean
  - useEffectOnce
  - useFetch
  - useInterval
  - useEventListener
  - useLocalStorage
  - useDarkMode
- swr
- react-query
 -->

## React Hook이란?

React Hook은 함수 컴포넌트에서 React 상태와 생명주기 기능을 `연결(hook into)`할 수 있게 해주는 기능이다. 클래스 컴포넌트 없이 상태 관리와 사이드 이펙트를 처리할 수 있게 해주며, 코드를 재사용하고 구성하기 쉽게 만들어준다.

## 주요 Hooks

### useState

`useState`는 컴포넌트에서 상태를 관리하기 위한 Hook이다. 초기 상태값을 인자로 받고, 상태값과 그 값을 설정하는 함수를 쌍으로 반환한다.

```jsx
const [count, setCount] = useState(0);
```

### useEffect

`useEffect`는 컴포넌트가 렌더링될 때마다 특정 작업을 수행할 수 있게 해주는 Hook이다. 데이터 fetching, 구독 설정, 수동 DOM 조작 등의 사이드 이펙트를 처리할 때 사용한다.

```jsx
function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]); // count가 바뀔 때만 이 effect를 재실행한다.

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

### useContext

`useContext`는 React 컨텍스트(Context)에 저장된 현재 값에 접근할 수 있게 해주는 Hook이다. 컨텍스트를 통해 prop drilling 없이 컴포넌트 트리를 통해 데이터를 전달할 수 있다.

```jsx
const ThemeContext = React.createContext('light');

function Example() {
  const theme = useContext(ThemeContext);
  return <div theme={theme}>Theme is {theme}</div>;
}
```

### useRef

`useRef`는 ref 객체를 생성하는 Hook이다. 이 객체는 컴포넌트의 전 생애주기 동안 동일한 메모리를 참조한다. 주로 DOM에 직접 접근할 때 사용한다.

```jsx
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    // `current`는 실제 DOM 요소를 가리킨다.
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}

```

### useLayoutEffect

`useLayoutEffect`는 DOM 변경 후에 동기적으로 호출되는 Hook이다. DOM 변경에 따른 추가적인 렌더링을 방지하기 위해 사용한다. `useEffect`와 유사하지만, 레이아웃 계산을 수행하고 추가적인 렌더링을 방지하기 위해 사용한다.

```jsx
function Example() {
  const inputRef = useRef();

  useLayoutEffect(() => {
    inputRef.current.value = 'Hello';
  }, []);

  return <input ref={inputRef} />;
}
```

### useEffect vs useLayoutEffect

`useEffect`와 `useLayoutEffect`는 둘 다 React에서 사이드 이펙트를 처리하기 위한 Hook이지만, 실행 시점에 차이가 있어 서로 다른 사용 사례에 적합하다. 이 차이를 이해하기 위해서는 먼저 브라우저의 렌더링 과정을 알아야 한다. 브라우저는 DOM을 업데이트하고 스타일을 계산한 후, 페이지에 변화를 그리는(렌더링하는) 과정을 거친다.

#### useEffect?

`useEffect`는 컴포넌트가 렌더링된 후에 비동기적으로 실행된다.
이는 브라우저가 화면을 그리는 작업이 완료된 후에 실행되므로, `useEffect` 내부에서 수행하는 작업이 화면 업데이트를 유발하더라도 사용자가 "깜빡임"을 감지하지 못할 수 있다. 따라서, `useEffect`는 데이터 fetching, 이벤트 리스너 등록, 직접적인 DOM 조작 같은 사이드 이펙트를 처리하는 데 주로 사용된다. 그러나 이러한 비동기적 실행으로 인해 화면에 이미 변화가 반영된 후에 코드가 실행되므로, DOM의 레이아웃을 계산하거나 조정하는 작업에는 적합하지 않을 수 있다.

#### useLayoutEffect?

반면, `useLayoutEffect`는 DOM 변경 사항이 화면에 반영되기 직전, 즉 브라우저가 화면을 그리기 전에 동기적으로 실행된다. 이는 `useEffect`와 달리, 실행 타이밍이 화면 업데이트 과정 중에 위치하기 때문에, `useLayoutEffect` 내에서 수행하는 작업으로 인한 추가적인 렌더링이 사용자에게 보이지 않는다.

예를 들어, *요소의 초기 포커스* 설정, *요소의 크기나 위치를 계산하여 스타일을 동적으로 변경*하는 작업 등이 이에 해당한다.

#### 비교해보기

- 실행 시점:
  - `useEffect`는 비동기적으로, 화면 업데이트 후에 실행된다.
  - `useLayoutEffect`는 동기적으로, 화면 업데이트 바로 전에 실행된다.

- 사용 사례:
  - useEffect: 데이터 fetching, 이벤트 리스너 등록/해제, 비동기 작업.
  - useLayoutEffect: DOM의 크기나 위치 계산, 요소에 대한 동적 스타일 적용, 초기 포커스 설정 등 레이아웃 조정.

- 성능 영향: 불필요한 `useLayoutEffect` 사용은 렌더링 성능에 부정적인 영향을 줄 수 있다. 가능하면 `useEffect` 사용을 우선 고려하되, 레이아웃 조정이 필요한 경우에 `useLayoutEffect`를 사용한다.

결국, 두 Hook의 주요 차이는 "언제 실행되느냐"에 있다. `useEffect`는 사용자에게 보이는 화면 업데이트 후에 실행되어 사이드 이펙트 처리에 적합하고, `useLayoutEffect`는 화면 업데이트 전에 실행되어 DOM 레이아웃 조정 작업에 적합하다.

## React StrictMode란

`React StrictMode`는 React 애플리케이션의 잠재적 문제를 발견하기 위해 개발 모드에서 사용할 수 있는 도구이다. 부모 컴포넌트 내에서 자식 컴포넌트들에 대해 엄격한 검사를 활성화하여, 부적절한 생명주기 메서드의 사용, 레거시 API의 사용 등을 경고한다.

## Hook의 규칙

Hook은 두 가지 주요 규칙을 따라야 한다

1. 최상위에서만 Hook을 호출해야 한다. 반복문, 조건문, 중첩된 함수 내에서 Hook을 실행하면 안 된다.
2. React 함수 컴포넌트와 커스텀 Hook 내에서만 Hook을 호출해야 한다.

이 규칙들은 Hook의 상태와 생명주기가 예측 가능한 방식으로 동작하도록 보장한다.

>**참고 링크**
>
>- [React 공식 문서: React Hooks](https://react.dev/reference/react/hooks)
>- [React StrictMode](https://react.dev/reference/react/StrictMode)
