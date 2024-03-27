# week-6

## [관심사의 분리 (Separation of Concerns, SoC)](https://en.wikipedia.org/wiki/Separation_of_concerns)

관심사의 분리는 소프트웨어 설계의 핵심 원칙 중 하나로, 애플리케이션을 명확하게 구분된 기능적 단위로 나누는 것을 말한다. 이를 통해 각 부분은 독립적으로 개발, 최적화, 유지보수될 수 있으며, 전체 시스템의 복잡성을 관리할 수 있다.

## [Layered Architecture](https://docs.microsoft.com/en-us/previous-versions/msp-n-p/ee658117(v=pandp.10))

계층형 아키텍처는 소프트웨어를 명확히 구분된 여러 계층으로 구성하는 아키텍처 패턴이다. 일반적으로 프레젠테이션, 비즈니스 로직, 데이터 액세스 계층으로 구분된다. 이러한 관심사의 분리로 인해 각 계층은 독립적으로 개발 및 수정될 수 있다.

## [Flux Architecture](https://facebook.github.io/flux/)

Flux는 클라이언트 사이드 웹 애플리케이션을 구축하기 위한 아키텍처 패턴으로, Facebook이 제안했다. 이는 단방향 데이터 흐름을 갖는 이벤트 주도 아키텍처로, 애플리케이션의 상태 관리를 용이하게 한다.

## [useReducer](https://react.dev/reference/react/useReducer)

`useReducer`는 React의 훅 중 하나로, 컴포넌트의 상태 관리 로직을 리듀서로써 구현할 수 있게 해준다. 이는 복잡한 상태 로직을 다룰 때 `useState`보다 더 적합할 수 있으며, Flux 아키텍처 패턴의 일부로 볼 수 있다.

## [useCallback](https://react.dev/reference/react/useCallback)

`useCallback`은 React의 훅으로, 메모이제이션된 콜백 함수를 반환한다. 이 훅은 특정 종속성이 변경되었을 때만 함수를 다시 생성하게 하여, 불필요한 렌더링을 방지하고 성능을 최적화하는 데 유용하다.

## [TSyringe](https://github.com/microsoft/tsyringe)

TSyringe는 TypeScript에서 사용할 수 있는 가벼운 의존성 주입 라이브러리이다. 이는 클래스의 생성자를 통해 자동으로 의존성을 주입해주며, 코드의 모듈성과 테스트 용이성을 향상시킨다.

## 의존성 주입 (Dependency Injection, DI)

의존성 주입은 객체가 필요로 하는 의존성을 외부에서 제공하는 디자인 패턴이다. 이는 객체 간의 결합도를 낮추고, 코드의 재사용성 및 테스트 용이성을 향상시킨다.

## [reflect-metadata](https://github.com/rbuckton/reflect-metadata)

`reflect-metadata`는 TypeScript와 함께 사용되는 라이브러리로, 런타임에 메타데이터를 읽고 쓸 수 있게 해준다. 이는 TSyringe와 같은 의존성 주입 라이브러리에서 클래스와 멤버에 대한 메타데이터를 활용할 때 중요한 역할을 한다.

## [singleton (싱글톤)](https://refactoring.guru/design-patterns/singleton)

싱글톤은 소프트웨어 디자인 패턴의 하나로, 특정 클래스의 인스턴스가 하나만 생성되고, 애플리케이션의 어디서든 그 인스턴스에 접근할 수 있도록 하는 구조이다. 이 패턴은 전역 상태를 관리하거나, 리소스 공유가 필요한 상황에 주로 사용된다.

## [Redux](https://redux.js.org/)

Redux는 JavaScript 앱의 상태 관리를 위한 라이브러리로, React와 함께 사용하기 좋게 설계되었다. Redux는 애플리케이션의 상태를 전역적으로 관리하는 스토어를 제공하며, 상태 변경은 순수 함수인 리듀서를 통해 이루어진다. Flux 아키텍처를 기반으로 하며, 예측 가능한 상태 관리를 가능하게 한다.

## [Reflect](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect)

Reflect는 JavaScript의 Reflection API의 일부로, 런타임에 객체를 조사하고 조작하는 메서드를 제공한다. `reflect-metadata`와 함께 사용되어, 타입스크립트 데코레이터와 메타데이터를 활용하는 데 유용한다.

## [usestore-ts](https://www.npmjs.com/package/usestore-ts)

리액트 상태관리 라이브러리 (made by Ashal)

## [useSyncExternalStore](https://react.dev/reference/react/useSyncExternalStore)

`useSyncExternalStore`는 React 18에서 도입된 훅으로, 외부 데이터 소스와 동기화된 상태를 React 컴포넌트에서 사용할 수 있게 한다. 이 훅은 Redux와 같은 외부 상태 관리 라이브러리와의 통합을 개선하기 위해 설계되었다.
