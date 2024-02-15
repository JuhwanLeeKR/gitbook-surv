# react state

## React State

**React State**는 컴포넌트 내에서 관리되는 동적 데이터의 집합이자 상태를 저장하고 관리하는 메커니즘이다.
상태는 앱 내에서 사용자 상호작용이나 시간의 경과에 따라 변경될 수 있는 모든 데이터를 포함한다. React는 상태가 변경될 때마다 해당 컴포넌트와 그 자식 컴포넌트를 효율적으로 다시 렌더링하여 UI를 최신 상태로 유지한다.

이 과정에서 React는 가상 DOM을 사용하여 실제 DOM에 적용할 최소한의 변경 사항을 계산한다. 이러한 방식은 앱의 성능을 최적화하고, 개발자가 상태 관리에 집중할 수 있게 해준다. (React는 가상 DOM 2개를 유지하고 있다, 깊은 학습을 위해서는 diffing 알고리즘에 대해 알아보길 추천한다)

클래스 컴포넌트에서는 `this.setState()` 메서드를 통해 상태를 업데이트하며, 함수형 컴포넌트에서는 `useState` Hook을 사용한다.

## useState

**useState**는 React의 Hook 중 하나로, 함수형 컴포넌트에서 상태 관리를 위해 사용된다.

`useState` Hook을 사용하면 초기 상태를 설정하고, 그 상태를 업데이트하는 함수를 반환한다. 이 함수는 이전 상태값을 참조하여 새 상태값을 설정할 수 있게 해준다.

복잡한 상태 로직을 관리할 때는 상태 업데이트 함수에 콜백 형태로 이전 상태를 전달함으로써, 상태 업데이트가 이전 상태에 기반하도록 할 수 있다.
또한, 배열이나 객체와 같은 복잡한 데이터 구조를 상태로 관리할 때는 상태를 업데이트할 때마다 상태의 불변성을 유지하는 것이 중요하다.

- `useState`를 사용한 함수형 컴포넌트에서의 상태 관리

```jsx
function Counter() {
  const [count, setCount] = useState(0);

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

## DRY 원칙

**DRY 원칙 ("Don't Repeat Yourself")**은 코드 중복을 최소화하여 소프트웨어 개발 과정에서의 정보의 중복을 방지하고, 재사용성을 높이는 원칙이다.

중복된 코드가 여러 곳에 존재하면, 변경사항이 발생했을 때 모든 부분을 찾아 수정해야 하는 번거로움과 오류 발생 가능성이 높아진다. DRY 원칙을 따르면 유지보수가 용이해지고 코드의 일관성을 유지할 수 있다.

**DRY 원칙**을 적용하는 가장 좋은 방법 중 하나는 함수와 컴포넌트의 재사용을 최대화하는 것이다.

예를 들어, 여러 컴포넌트에서 공통으로 사용되는 유틸리티 함수나 UI 컴포넌트를 생성하여 중복 코드를 제거할 수 있다.
코드 리팩토링 과정에서 비슷한 로직을 발견하면, 이를 추상화하여 재사용 가능한 함수나 컴포넌트로 분리하는 것이 좋다.

## SSOT (Single Source of Truth)

**SSOT**는 데이터 관리 원칙 중 하나로, 모든 데이터가 하나의 출처에서만 관리되어야 한다는 개념이다.

이 원칙은 데이터의 일관성과 신뢰성을 유지하고, 데이터 관리의 복잡성을 줄이는 데 중요하다.
SSOT를 적용하면, 데이터 변경 시 단일 출처를 업데이트함으로써 전체 시스템에서 데이터의 일관성을 보장할 수 있다.

- 데이터베이스에서의 사용자 정보 관리 (예시)
  - 사용자 정보가 여러 테이블이나 데이터베이스에 걸쳐 중복되어 저장되지 않고, 하나의 사용자 정보 테이블에만 저장되어 관리된다.
  - 사용자의 주소 변경 같은 데이터 업데이트가 필요할 때, 단 하나의 테이블만 업데이트함으로써 모든 시스템에서 최신의 일관된 정보를 반영할 수 있다.

### SSOT의 원칙을 따르기

**SSOT**의 원칙을 따르는 한 가지 방법은 모든 데이터 관련 작업을 중앙화된 데이터 관리 시스템을 통해 처리하는 것이다.

예를 들어, 애플리케이션의 상태 관리를 위해 Redux나 MobX와 같은 상태 관리 라이브러리를 사용하면, 애플리케이션의 모든 상태를 한 곳에서 관리할 수 있다.

이러한 접근 방식은 데이터의 일관성을 보장하고, 데이터 관련 버그의 가능성을 줄일 수 있다.

## 1급 객체 (First-Class Object)

프로그래밍 언어에서 **1급 객체**는 다른 객체들에 적용 가능한 연산(변수 할당, 함수 인자 전달, 반환 값으로 사용)을 모두 지원하는 객체를 의미한다.
1급 객체로 취급되는 것은 해당 언어의 유연성을 크게 향상시킨다.

- JavaScript에서의 함수

```javascript
// JavaScript에서 함수는 1급 객체로 취급된다. 이는 함수를 변수에 할당할 수 있음을 의미한다.
const greet = function(name) {
  console.log("Hello, " + name);
};

// 함수를 다른 함수의 인자로 전달할 수 있다.
function greetSomeone(greetingFunction, name) {
  greetingFunction(name);
}
greetSomeone(greet, "World"); // 출력: Hello, World

// 함수에서 다른 함수를 반환할 수 있다.
function getGreetingFunction() {
  return function(name) {
    console.log("Hello, " + name);
  };
}
const greetWorld = getGreetingFunction();
greetWorld("World"); // 출력: Hello, World
```

이러한 특성 덕분에 JavaScript에서 함수는 매우 유연하게 사용될 수 있으며,
고차 함수(Higher-Order Function)와 같은 고급 프로그래밍 패턴을 가능하게 한다.

### 1급 객체의 중요성

프로그래밍 언어에서 **1급 객체**로서의 함수는 코드의 추상화 수준을 높이고, 더 표현력 있는 프로그래밍을 가능하게 한다.

함수형 프로그래밍 패러다임에서는 이러한 특성을 활용하여 데이터를 변형하는 데 필요한 작업을 함수의 조합으로 표현한다.
예를 들어, 배열의 `map`, `filter`, `reduce` 같은 고차 함수는 다른 함수를 인자로 받아 복잡한 데이터 처리 작업을 간결하게 표현할 수 있게 해준다.

## Lifting State Up

**Lifting State Up** 패턴은 여러 컴포넌트가 동일한 상태를 공유해야 할 때 사용된다.

이 패턴을 사용할 때는 상태를 갖는 컴포넌트와 이 상태를 필요로 하는 모든 자식 컴포넌트 사이의 가장 가까운 공통 조상 컴포넌트를 찾아 그곳에 상태를 배치한다.
그 후, 상태를 업데이트하는 함수와 상태 자체를 자식 컴포넌트에게 props로 전달한다.

이 방법은 상태를 필요로 하는 모든 컴포넌트가 일관된 상태를 유지할 수 있도록 하며, 상태 관리의 복잡성을 줄이는 데 도움이 된다.

```jsx
import React, { useState } from 'react';

function ParentComponent() {
  const [sharedState, setSharedState] = useState(0);

  // 상태 증가 함수
  const handleIncrementState = () => setSharedState(prevState => prevState + 1);
  // 상태 감소 함수
  const handleDecrementState = () => setSharedState(prevState => prevState - 1);

  return (
    <div>
      <h2>Parent Shared State: {sharedState}</h2>
      <ChildComponentA sharedState={sharedState} handleIncrementState={handleIncrementState} />
      <ChildComponentB sharedState={sharedState} handleDecrementState={handleDecrementState} />
    </div>
  );
}

function ChildComponentA({ sharedState, handleIncrementState }) {
  return (
    <div>
      <p>Child A State: {sharedState}</p>
      <button onClick={handleIncrementState}>Increase</button>
    </div>
  );
}

function ChildComponentB({ sharedState, handleDecrementState }) {
  return (
    <div>
      <p>Child B State: {sharedState}</p>
      <button onClick={handleDecrementState}>Decrease</button>
    </div>
  );
}
```

>**참고 링크**
>
>- [React 공식 문서](https://reactjs.org/docs/getting-started.html)
>- [DRY 원칙](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
>- [SSOT](https://en.wikipedia.org/wiki/Single_source_of_truth)
>- [useState Hook](https://reactjs.org/docs/hooks-state.html)
>- [1급 객체](https://en.wikipedia.org/wiki/First-class_citizen)
>- [Lifting State Up](https://reactjs.org/docs/lifting-state-up.html)
