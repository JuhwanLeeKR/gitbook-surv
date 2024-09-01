# hooks

## useEffect() 기명 함수와 함께 사용하기

```jsx
// 기명 함수
function namedFunction(params) {
  // some logic
}

useEffect(function isInViewSomeComponent() {
  if (isInView(someRef.current)) {
    // some logic
  }
}, [isInView])

useEffect(function onInit() {
  if (!isInit) {
    return
  }

  setIsInit(false)
}, [isInit])

/**
 * 에러가 터졌을 때
 * 1. console.log
 * 2. report
 * 3. monitoring
 * 4. React Devtools
 *
 * => Log
 * */
useEffect(function addEvent() {
  document.addEventListener()

  return function removeEvent() {
    document.removeEventListener()
  }
}, [isInit])
```

## 한 가지 역할만 수행하는 useEffect()

- SRP (단일 책임 원칙): 하나의 역할만 수행하는 무언가를 만들자 (useEffect도 그렇게 만들자)

- useEffect()
- 한가지의 역할만 하고 있나?

- 방법은?
  - 기명 함수를 사용해보자
  - dependency array에 너무 많은 관찰 대상이 들어가고 있는 게 아닌가?

```jsx
const LoginPage = ({token, newPath}) => { // ❌
  useEffect(() => {
    redirect(newPath)

    const userInfo = setLogin(token)
    // .. 로그인 로직
  }, [token, newPath])

  return <div></div>
}
```

- 경로가 바꼈는데 로그인 로직을 탈 수도 있고
- 토큰이 바뀌었는데, redirect가 동작할 수 있다.

```jsx
// 분리 후 필요하다면 bridge 로직을 넣어주면 됨
const LoginPage = ({token, newPath}) => { // ✅
  useEffect(() => {
    redirect(newPath)
  }, [newPath])

  useEffect(() => {
    const userInfo = setLogin(token)
    // .. 로그인 로직
  }, [token])

  return <div></div>
}
```

## Custom Hooks 반환의 종류

```jsx
const ReturnCustomHooks = () => {
  //❌ getter와 setter의 위치가 변경됨
  const [setValue, value] = useSomeHooks(true)
  //❌ 하나의 value면 배열로 내보내지 말고 값으로 내보낸다
  const [oneValue] = useSomeHooks()
  //❌
  const [firstValue, secondValue, _, thirdValue, _, setValue]= useSomeHooks(true)
  //❌ 구조 분해 할당을 사용하는 것이 더 낫다
  const query = useQuery({queryKey: ['hello'], queryFn: getHello})

  const data = query.data
  const refetch = query.refetch
  const isSuccess = query.isSuccess


  return (
    // some logic
  )
}
```

## useEffect() 내부의 비동기

- useEffect 내부에서는 비동기 함수가 불가능하다

```jsx
// ❌
useEffect(async () => {
  // 비동기 작업
  const result = await fetchData()
},[])
```

```jsx
// ✅
useEffect(() => {
  // 비동기 작업
  const fetchData = async () => {
    const result = await someFetch()
  }

  fetchData()
},[dependency])
```
