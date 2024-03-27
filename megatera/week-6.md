# week-6

## [관심사의 분리 (Separation of Concerns, SoC)](https://en.wikipedia.org/wiki/Separation_of_concerns)

관심사의 분리는 소프트웨어 설계의 핵심 원칙 중 하나로, 애플리케이션을 명확하게 구분된 기능적 단위로 나누는 것을 말한다. 이를 통해 각 부분은 독립적으로 개발, 최적화, 유지보수될 수 있으며, 전체 시스템의 복잡성을 관리할 수 있다.

- 장점: 코드의 재사용성 및 유지 보수성이 향상된다. 각 기능별로 구분되어 있기 때문에, 문제 발생 시 해당 기능만을 분리해 수정할 수 있다.
- 단점: 과도한 분리는 애플리케이션의 구조를 복잡하게 만들 수 있으며, 때로는 성능 저하를 초래할 수도 있다.

```ts
// UI 관련 코드
function renderUserInterface(user: User) {
  console.log(`Displaying user interface for ${user.name}`);
}

// 데이터 처리 코드
function fetchUserData(userId: string): User {
  // 데이터베이스에서 사용자 데이터를 조회하는 로직 (e.g. fetch)
  return { id: userId, name: "John Doe" };
}

// 비즈니스 로직
function processUserLogin(userId: string) {
  const user = fetchUserData(userId);
  renderUserInterface(user);
}
```

## [Layered Architecture](https://docs.microsoft.com/en-us/previous-versions/msp-n-p/ee658117(v=pandp.10))

계층형 아키텍처는 소프트웨어를 명확히 구분된 여러 계층으로 구성하는 아키텍처 패턴이다. 일반적으로 프레젠테이션, 비즈니스 로직, 데이터 액세스 계층으로 구분된다. 이러한 관심사의 분리로 인해 각 계층은 독립적으로 개발 및 수정될 수 있다.

- 장점: 각 계층이 독립적이기 때문에, 유지 보수 및 테스트가 용이하며, 다른 시스템과의 통합도 쉽게 할 수 있다.
- 단점: 계층 간의 호출이 많아질 수 있으며, 때로는 시스템의 성능에 영향을 줄 수 있다. 또한, 설계 초기에 계층을 잘못 설정하면 나중에 변경하기 어려울 수 있다.

```ts
// 데이터 액세스 계층
class UserDataAccess {
  getUserById(userId: string): User {
    // DB에서 사용자 정보를 조회하는 로직
    return new User();
  }
}

// 비즈니스 로직 계층
class UserService {
  private userDataAccess = new UserDataAccess();

  getUser(userId: string): User {
    return this.userDataAccess.getUserById(userId);
  }
}

// 프레젠테이션 계층
class UserController {
  private userService = new UserService();

  displayUser(userId: string) {
    const user = this.userService.getUser(userId);
    console.log(`User: ${user.name}`);
  }
}

```

## [Flux Architecture](https://facebook.github.io/flux/)

Flux는 클라이언트 사이드 웹 애플리케이션을 구축하기 위한 아키텍처 패턴으로, Facebook이 제안했다. 이는 단방향 데이터 흐름을 갖는 이벤트 주도 아키텍처로, 애플리케이션의 상태 관리를 용이하게 한다.

- 장점:
  - 예측 가능한 데이터 흐름: 단방향 데이터 흐름으로 인해 애플리케이션 상태가 어떻게 변경되는지 쉽게 이해할 수 있다.
  - 디버깅 용이: 상태 변경의 원인이 되는 Action을 추적하기 쉽기 때문에, 디버깅이 용이하다.
모듈성: 각 구성 요소의 역할이 명확히 분리되어 있어, 시스템의 모듈성이 높아진다.
- 단점:
  - 보일러플레이트 코드: 많은 구성 요소와 연결 과정이 필요하기 때문에, 초기 설정에 많은 코드가 필요할 수 있다.
  - 러닝 커브: Flux 아키텍처의 개념과 데이터 흐름을 이해하는 데 시간이 필요할 수 있다.

```ts
// Action 정의
interface Action {
  type: string;
  payload?: any;
}

// Dispatcher 구현
class Dispatcher {
  dispatch(action: Action) {
    console.log(`Action dispatched: ${action.type}`);
    // Store 업데이트 로직 구현
  }
}

// Store 구현
class Store {
  private state: any;

  constructor(private dispatcher: Dispatcher) {
    // Dispatcher를 통해 Action을 받아 상태를 업데이트
  }

  getState() {
    return this.state;
  }
}

// View에서 Store의 상태를 사용
const dispatcher = new Dispatcher();
const store = new Store(dispatcher);

dispatcher.dispatch({ type: 'ACTION_TYPE', payload: 'data' });
console.log(store.getState());
```

## [useReducer](https://react.dev/reference/react/useReducer)

`useReducer`는 React의 훅 중 하나로, 컴포넌트의 상태 관리 로직을 리듀서로써 구현할 수 있게 해준다. 이는 복잡한 상태 로직을 다룰 때 `useState`보다 더 적합할 수 있으며, Flux 아키텍처 패턴의 일부로 볼 수 있다.

- 장점:
  - 중앙 집중식 상태 관리: 상태 업데이트 로직을 컴포넌트 바깥에 두어 관리하기 편리하다.
  - 성능 최적화: 연관된 컴포넌트만 리렌더링하므로 성능 최적화에 유리하다.
  - 테스트 용이: 리듀서 함수는 순수 함수이기 때문에 독립적으로 테스트하기가 용이하다.
- 단점:
  - 초기 러닝 커브: useState보다 복잡하여, 학습하는 데 시간이 필요할 수 있.
  - 보일러플레이트 코드 증가: 작은 컴포넌트나 간단한 상태 관리에는 과도한 설정이 필요할 수 있.

```tsx
import React, { useReducer } from 'react';

interface State {
  count: number;
}

type Action = { type: 'increment' } | { type: 'decrement' };

function reducer(state: State, action: Action): State {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

const Counter = () => {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </>
  );
};

export default Counter;
```

## [useCallback](https://react.dev/reference/react/useCallback)

`useCallback`은 React의 훅으로, 메모이제이션된 콜백 함수를 반환한다. 이 훅은 특정 종속성이 변경되었을 때만 함수를 다시 생성하게 하여, 불필요한 렌더링을 방지하고 성능을 최적화하는 데 유용하다.

```tsx
import React, { useCallback, useState } from 'react';

const IncrementButton = ({ increment }: { increment : () => void}) => {
  console.log('IncrementButton rendered');
  return <button onClick={increment}>Increment</button>;
};

const Counter = () => {
  const [count, setCount] = useState(0);

  // count가 변경될 때만 increment 함수를 재생성
  const increment = useCallback(() => {
    setCount(c => c + 1);
  }, [setCount]); // setCount는 변경되지 않으므로 사실상 재생성되지 않음

  return (
    <div>
      <div>Count: {count}</div>
      <IncrementButton increment={increment} />
    </div>
  );
};

export default Counter;
```

## [TSyringe](https://github.com/microsoft/tsyringe)

TSyringe는 TypeScript에서 사용할 수 있는 가벼운 의존성 주입 라이브러리이다. 이는 클래스의 생성자를 통해 자동으로 의존성을 주입해주며, 코드의 모듈성과 테스트 용이성을 향상시킨다.

- 장점:
  - 모듈성 향상: 애플리케이션의 결합도를 낮추고 모듈 간의 독립성을 강화한다.
  - 테스트 용이성: `Mock Objects`를 사용하여 단위 테스트가 용이하다.
  - 유연성: 구성 요소를 쉽게 교체하거나 업데이트할 수 있어, 유지 보수 및 확장성이 향상된다.
- 단점:
  - 리플렉션 사용으로 인해 미세한 성능 저하가 발생할 수 있고, 약간의 러닝 커브가 있을 수 있다.

```ts
import 'reflect-metadata';
import { container, injectable } from 'tsyringe';

interface IMessageService {
  sendMessage(message: string): void;
}

@injectable()
class EmailService implements IMessageService {
  sendMessage(message: string) {
    console.log(`Email sent: ${message}`);
  }
}

@injectable()
class NotificationService {
  constructor(private messageService: IMessageService) {}

  notify(message: string) {
    this.messageService.sendMessage(message);
  }
}

container.registerSingleton<IMessageService, EmailService>();

const notificationService = container.resolve(NotificationService);
notificationService.notify('Hello, world!');
```

## 의존성 주입 (Dependency Injection, DI)

의존성 주입은 객체가 필요로 하는 의존성을 외부에서 제공하는 디자인 패턴이다. 이는 객체 간의 결합도를 낮추고, 코드의 재사용성 및 테스트 용이성을 향상시킨다.

## [reflect-metadata](https://github.com/rbuckton/reflect-metadata)

`reflect-metadata`는 TypeScript와 함께 사용되는 라이브러리로, 런타임에 메타데이터를 읽고 쓸 수 있게 해준다. 이는 TSyringe와 같은 의존성 주입 라이브러리에서 클래스와 멤버에 대한 메타데이터를 활용할 때 중요한 역할을 한다.

- 장점:
  - 메타 데이터 기반 프로그래밍 지원: 클래스, 메서드, 프로퍼티에 대한 메타 데이터를 정의하고, 런타임에 이를 조회할 수 있어, 메타 데이터 기반의 고급 프로그래밍 패턴 구현을 가능하게 한다.
  - 의존성 주입 용이: `reflect-metadata`를 사용하면, 타입 정보를 기반으로 자동으로 의존성을 주입할 수 있어, DI 구현이 용이해진다.
  - 유연성과 확장성: 데코레이터와 메타 데이터를 활용하여 유연하고 확장 가능한 애플리케이션 아키텍처를 구성할 수 있다.
- 단점:
  - 메타 데이터 조회와 조작은 런타임 성능에 영향을 줄 수 있으므로, 성능이 중요한 애플리케이션에서는 사용 시 주의가 필요하다.

```ts
import 'reflect-metadata';

// 클래스에 메타 데이터 첨부
@Reflect.metadata('role', 'admin')
class User {}

console.log(Reflect.getMetadata('role', User)); // 'admin'

// 메서드 파라미터에 메타 데이터 첨부
class Product {
    @Reflect.metadata('validate', true)
    updatePrice(price: number) {
        console.log(`Updating price to ${price}`);
    }
}

const isValidate = Reflect.getMetadata('validate', Product.prototype, 'updatePrice');
console.log(isValidate); // true
```

## [singleton (싱글톤)](https://refactoring.guru/design-patterns/singleton)

싱글톤은 소프트웨어 디자인 패턴의 하나로, 특정 클래스의 인스턴스가 하나만 생성되고, 애플리케이션의 어디서든 그 인스턴스에 접근할 수 있도록 하는 구조이다. 이 패턴은 전역 상태를 관리하거나, 리소스 공유가 필요한 상황에 주로 사용된다.

```ts
class DatabaseConnection {
    private static instance: DatabaseConnection;

    private constructor() {
        // 생성자를 private으로 선언하여 외부에서의 인스턴스화 방지
    }

    public static getInstance(): DatabaseConnection {
        if (!DatabaseConnection.instance) {
            DatabaseConnection.instance = new DatabaseConnection();
        }
        return DatabaseConnection.instance;
    }

    public query(sql: string) {
        console.log(`Executing query: ${sql}`);
        // 데이터베이스 쿼리 실행 로직
    }
}

const instance = DatabaseConnection.getInstance();
instance.query("SELECT * FROM users");
```

## [Redux](https://redux.js.org/)

Redux는 JavaScript 앱의 상태 관리를 위한 라이브러리로, React와 함께 사용하기 좋게 설계되었다. Redux는 애플리케이션의 상태를 전역적으로 관리하는 스토어를 제공하며, 상태 변경은 순수 함수인 리듀서를 통해 이루어진다. Flux 아키텍처를 기반으로 하며, 예측 가능한 상태 관리를 가능하게 한다.

- 장점:
  - 예측 가능한 상태 관리: Redux는 애플리케이션의 모든 상태 변화를 중앙 집중화된 스토어를 통해 관리하기 때문에, 상태 변화의 추적과 관리가 용이하다.
  - 유지보수성 향상: 상태 관리 로직이 한 곳에 모여 있어, 코드의 구조를 이해하기 쉽고 유지보수하기 편리하다.
  - 디버깅 용이: Redux DevTools와 같은 도구를 사용하면, 상태 변화의 기록을 쉽게 확인하고, 시간 여행 디버깅이 가능하다.
- 단점:
  - 액션 타입 선언, 액션 생성자, 리듀서 등을 정의해야 하므로, 상대적으로 많은 초기 설정 코드가 필요하다.

```ts
import { createStore, combineReducers, Action } from 'redux';

// 액션 타입 정의
const INCREMENT = 'INCREMENT';
const DECREMENT = 'DECREMENT';

// 액션 생성 함수
const increment = () => ({ type: INCREMENT });
const decrement = () => ({ type: DECREMENT });

// 리듀서
interface CounterState {
  count: number;
}

const initialCounterState: CounterState = { count: 0 };

function counterReducer(state = initialCounterState, action: Action<string>): CounterState {
  switch (action.type) {
    case INCREMENT:
      return { ...state, count: state.count + 1 };
    case DECREMENT:
      return { ...state, count: state.count - 1 };
    default:
      return state;
  }
}

// 스토어 생성
const rootReducer = combineReducers({ counter: counterReducer });
const store = createStore(rootReducer);

// 사용 예
store.dispatch(increment()); // count를 증가시킴
console.log(store.getState().counter); // { count: 1 }

```

## [Reflect](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect)

Reflect는 JavaScript의 Reflection API의 일부로, 런타임에 객체를 조사하고 조작하는 메서드를 제공한다. `reflect-metadata`와 함께 사용되어, 타입스크립트 데코레이터와 메타데이터를 활용하는 데 유용하다.

- 장점:
  - 유연성 및 표현력 향상: 객체와 그 속성에 대한 더 세밀하고 동적인 작업을 가능하게 한다.
  - 일관된 API: `Reflect`는 자바스크립트의 메타 프로그래밍 기능을 일관된 방식으로 제공한다.
- 단점
  - 성능 고려: Reflection을 사용한 동적 프로그래밍은 직접적인 객체 조작보다 성능 오버헤드가 발생할 수 있다.
  - 복잡성 증가: 코드의 복잡성이 증가할 수 있으며, 오용할 경우 버그의 원인이 될 수 있다.

## [usestore-ts](https://www.npmjs.com/package/usestore-ts)

리액트 상태관리 라이브러리 (made by Ashal)

## [useSyncExternalStore](https://react.dev/reference/react/useSyncExternalStore)

`useSyncExternalStore`는 React 18에서 도입된 훅으로, 외부 데이터 소스와 동기화된 상태를 React 컴포넌트에서 사용할 수 있게 한다. 이 훅은 Redux와 같은 외부 상태 관리 라이브러리와의 통합을 개선하기 위해 설계되었다.

- 구독 기반 모델을 사용하여, 필요할 때만 컴포넌트를 리렌더링한다.

```tsx
import { useSyncExternalStore } from 'react';

// 외부 상태 소스를 구독하는 함수
function subscribeToExternalStore(callback) {
  externalStore.subscribe(callback);
  return () => externalStore.unsubscribe(callback);
}

// 외부 상태 소스에서 현재 상태를 가져오는 함수
function getExternalStoreState() {
  return externalStore.getState();
}

function MyComponent() {
  // useSyncExternalStore를 사용하여 외부 상태 소스와 동기화
  const state = useSyncExternalStore(subscribeToExternalStore, getExternalStoreState);

  return <div>{state}</div>;
}

```
