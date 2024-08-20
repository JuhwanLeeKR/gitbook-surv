# state

## 상태 소개

### 점점 어려워지는 상태관리가 문제일까? 상태를 대하는 태도가 문제일까?

- 컴포넌트 상태
- 전역 상태
- 서버 상태
- 상태 변경
- 상태 최적화
- 렌더링 최적화
- 불변성
- 상태 관리자

### 우리는 상태관리를 왜 하고 있는 것일까?

- 상태 관리는 목적인가? 수단인가?
- 상태 관리를 위해 앱을 개발하는 것일까?
- 앱을 개발하는데 상태는 왜 관리하는 것일까?

### 상태(State)란?

- 사물 현상이 놓여 있는 모양이나 형편 (e.g. 신호등)4

## 올바른 초기값 설정

```js
const [list, setList] = useState() // ❌ 넣지 않으면 undefined
const [list, setList] = useState([]) // ✅
```

- 리액트 렌더링 오류는 내가 생각하는 것보다 여러 번 발생하고 그 속도, 순서를 제어할 수 없기 때문에 초기값은 중요하다

## 업데이트되지 않는 값

```js
const Func = () => {
  const CONSTANT = {
    1: 'hi'
    2: 'hello'
  }
  return <>
    <p>{CONSTANT}</p>
    <Comp constant={CONSTANT} />
  </>
}
```

상수를 다루거나 아니면 일반적인 방치
업데이트가 되지 않는 객체
리액트 상태로 바꾼다던가 아예 밖으로 내보내야 한다.

-> 컴포넌트가 생성될 때마다 상수가 계속 생성되기 때문에

## 플래그 상태

```js
const Comp = () => { // ❌
  const [isLogin, setIsLogin] = useState(false)

  useEffect(() => {
    if (a) {
      setIsLogin(true)
    }
    if (b) {
      setIsLogin(true)
    }

  },[a, b])
  return <></>
}
```

```js
const Comp = () => { // ✅
  const isLogin = a || b

  return <></>
}
```

- 플래그 값 : 주로 프로그래밍에서 특정 조건 혹은 제어를 위한 조건을 boolean으로 나타내는 값

플래그를 만들 때, useState를 쓰지 않고 컴포넌트 내부의 변수를 선언할 수 있다

## 불필요한 상태

```js
/**
 * 불필요한 상태를 만든다면?
 *
 * 결국에는 리액트에 의해 관리되는 값이 늘어나는 것
 * 그러다보면 렌더링에 영향을 주는 값이 늘어나서 관리 포인트가 더더욱 늘어난다.
 */

const Comp = () => { // ❌
  const [userList, setUserList] = useState(MOCK_DATA) // 초기 상태 선언
  const [complUserList, setComplUserList] = useState(MOCK_DATA) // 변경할 상태 선언

  useEffect(() => {
    const newList = compleUserList.filter((user) => user.completed === true)

    setUserList(newList)
  },[])

  return <></>
}
```

```js
const Comp = () => { // ✅
  const complUserList = complUserList.filter((user) => user.completed === true) // 내부에 변수를 사용하면 된다. 이 경우는 괜찮음

  return <></>
}
```

- props를 바로 useState에 쓰지 말고 return 문에 사용하자

- 리액트 컴포넌트내 변수는 렌더링 마다 고유의 값을 가지는 계산된 값 (Computed Value / 공식적인 명칭은 아님)

## 리렌더링 방지가 필요하다면 useState 대신 useRef

```js
const Comp = () => { // ❌ 리렌더링을 자주 발생시킬 수 있음
  const [isMount, setIsMount] = useState(false)

  useState(() => {
    if (!isMount) {
      setIsMount(true)
    }
  }, [isMount])

  return <></>
}
```

```js
const Comp = () => { // ✅
  const isMount = useRef(false)

  useEffect(() => {
    isMount.current = true

    return () => {
      isMount.current = false
    }
    // eslint rule 막기
  }, [])
  return <></>
}
```

컴포넌트의 전체적인 수명과 동일하게 지속된 정보를 일관적으로 제공해야하는 경우

## 연관된 상태 단순화하기

```js
const Comp = () => { // ❌
  const [isLoading, setIsLoading] = useState(false)
  const [isSuccess, setIsSuccess] = useState(false)
  const [isError, setIsError] = useState(false)

  if (isLoading) return <A />
  if (isSuccess) return <B />
  if (isError) return <C />
}
```

```js
const PROMISE_STATE = {
  INIT: 'init',
  LOADING: 'loading',
  SUCCESS: 'success',
  ERROR: 'error'
}

const Comp = () => { // ✅
  const [promiseState, setPromiseState] = useState(PROMISE_STATE.INIT)

  if (PROMISE_STATE.LOADING) return <A />
  if (PROMISE_STATE.SUCCESS) return <B />
  if (PROMISE_STATE.ERROR) return <C />
}
```

- KISS principle

Keep

It

Simple,

Stupid!

## 연관된 상태 객체로 묶어내기

```js
const Comp = () => { // ❌
  const [isLoading, setIsLoading] = useState(false)
  const [isSuccess, setIsSuccess] = useState(false)
  const [isError, setIsError] = useState(false)

  if (isLoading) return <A />
  if (isSuccess) return <B />
  if (isError) return <C />
}
```

```js
const Comp = () => { // ✅
  const [isFetch, setIsFetch] = useState({
    isLoading: false,
    isSuccess: false,
    isError: false,
  })

  if (isFetch.isLoading) return <A />
  if (isFetch.isSuccess) return <B />
  if (isFetch.isError) return <C />
}
```

## useState에서 useReducer로 리팩터링

```js
const INIT_STATE = {
  isLoading: false,
  isSuccess: false,
  isError: false
}

const ACTION_TYPE = {
  FETCH_LOADING: 'FETCH_LOADING',
  FETCH_SUCCESS: 'FETCH_SUCCESS',
  FETCH_ERROR: 'FETCH_ERROR'
}

// switch문을 권장하지만 if문도 가능하다
const reducer = (state, action) = {
  switch (action.type) {
    case 'FETCH_LOADING':
      return {isLoading: true, isSuccess: false, isError: false}
    case 'FETCH_SUCCESS':
      return {isLoading: false, isSuccess: true, isError: false}
    case 'FETCH_ERROR':
      return {isLoading: false, isSuccess: false, isError: true}
    default:
      return INIT_STATE
  }
}

const Comp = () => {
  const [state, dispatch] = useReducer(reducer, INIT_STATE)

  return <></>
}
```

- Recoil, Jotai, Zustand 쓰면 되지 않나?

순수 자바스크립트 문법으로 Third Party Library없이 상태를 관리할 수 있고, 그 상태를 조금 더 체계적으로 구조화할 수 있기 때문에 그 자체로 많은 무기로 활용할 수 있다

## 상태 로직 Custom Hooks로 뽑아내기

```js
const useFetchData = (url) => {
  const [state, dispatch] = useReducer(reducer, INIT_STATE)

  useEffect(() => {
    dispatch({ type: ACTION_TYPE.FETCH_LOADING})
    const fetchData = async () => {
      await fetch(url)
        .then(() => {
          dispatch({ type: ACTION_TYPE.FETCH_SUCCESS})
        }).catch(() => {
          dispatch({ type: ACTION_TYPE.FETCH_ERROR})
        })
    }
    fetchData()
  },[url])

  return state
}

const Comp = () => { // ✅
  const {isLoading, isSuccess, isError} = useFetchData(url)

  if (isLoading) return <A />
  if (isSuccess) return <B />
  if (isError) return <C />
}
```

## 이전 상태 활용하기

```js
const Comp = () => {
  const [age, setAge] = useState(10)

  const addAge1 = setAge(age + 1) // ❌
  const addAge2 = setAge((prevAge) => prevAge + 1) //✅

  return <></>
}
```
