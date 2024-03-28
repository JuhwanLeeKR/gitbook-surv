# week-7

## [HTML DOM API](https://developer.mozilla.org/ko/docs/Web/API/HTML_DOM_API)

`HTML DOM API`는 웹 문서의 객체 모델에 접근하고 조작할 수 있는 메서드와 속성의 모음이다. 웹 페이지의 구조, 스타일, 내용 등을 동적으로 변경할 수 있게 해준다. 이 API를 사용하면 자바스크립트를 통해 HTML 요소를 생성, 수정, 삭제하거나 이벤트를 처리할 수 있다.

> 선택: getElementById, querySelector, getElementsByClassName 등의 메서드를 사용하여 DOM 트리 내의 요소를 선택할 수 있다.
> 조작: 선택한 요소의 내용(innerHTML), 속성(setAttribute), 스타일(style) 등을 변경할 수 있다.
> 이벤트 처리: 요소에 이벤트 리스너(addEventListener)를 추가하여 사용자의 액션(클릭, 키보드 입력 등)에 반응할 수 있다.
> 생성 및 삭제: createElement, removeChild 등의 메서드를 사용하여 새로운 요소를 생성하거나 기존 요소를 삭제할 수 있다.

```js
// 요소 선택
const element = document.getElementById("myElement");
// 스타일 변경
element.style.color = "blue";
```

- 장점
  - 웹 페이지의 요소를 직접 조작하여 즉각적인 변화를 반영할 수 있다.
  - 순수 자바스크립트와 DOM API만으로 웹 페이지를 조작할 수 있어, 추가 라이브러리나 프레임워크가 없어도 사용할 수 있다.

- 단점
  - 큰 프로젝트에서 DOM을 직접 조작하면 코드가 복잡해지고 유지 관리가 어려워질 수 있다.
  - 대량의 DOM 조작은 웹 페이지의 성능을 저하시킬 수 있다.

DOM API는 웹 페이지의 동적 조작에 필수적이며, 자바스크립트를 사용한 웹 개발의 기본이 된다.
하지만, 복잡한 상호작용이나 대규모 DOM 조작이 필요한 애플리케이션에서는 React, Vue.js와 같은 현대적인 프론트엔드 프레임워크를 사용하는 것이 보다 효율적일 수 있다.
이러한 프레임워크는 성능 최적화, 상태 관리, 컴포넌트 기반 개발 등을 위한 추상화된 메커니즘을 제공하여 개발자가 보다 쉽게 복잡한 웹 애플리케이션을 구축할 수 있게 도와준다.

## Location, pathname

HTML DOM API의 `Location 객체는` 사용자의 현재 페이지의 URL을 나타내며, 여러 속성과 메소드를 제공한다. 이 중 `pathname` 속성은 URL의 경로 부분을 반환한다. 예를 들어, URL이 `http://www.example.com/about`일 경우, location.pathname의 값은 `/about`이 된다.

웹 페이지의 JavaScript에서 location.pathname을 사용하여 현재 페이지의 경로를 가져올 수 있다. 이 정보를 활용하여 페이지 로딩 시 특정 스크립트를 실행하거나, 사용자의 현재 위치에 따라 UI를 변경하는 등의 작업을 수행할 수 있다.

Location 객체는 pathname 외에도 href, search, hash 등 다양한 속성을 제공한다. 이러한 속성들을 활용하면 URL을 분석하고, 페이지를 리디렉션하며, 쿼리 문자열을 처리하는 등의 작업을 수행할 수 있다. 예를 들어, location.search는 URL의 쿼리 스트링을 반환하며, 이를 통해 GET 요청의 파라미터를 읽을 수 있다. 이런 다양한 속성과 메소드를 적절히 활용하면, 더욱 풍부하고 상호작용이 가능한 웹 페이지를 만들 수 있다.

```js
if (window.location.pathname === '/about') {
    // 특정 경로일 때 실행할 코드
    console.log('About 페이지에 있습니다.');
}
```

- 장점
  - URL의 특정 부분에 쉽게 접근할 수 있어 웹 개발 시 유용하게 사용할 수 있다.
  - `모든 주요 브라우저에서 지원`되므로, 크로스 브라우징 이슈 없이 사용할 수 있다.
  - 사용자가 현재 어떤 페이지에 있는지에 따라 동적으로 내용을 변경할 수 있어, SPA(Single Page Application) 개발에 유리하다.

- 단점
  - 특별히 명시적인 단점은 없지만, 보안 문제로 인해 사용자가 조작할 수 있는 URL의 일부(예: 해시(#) 이후의 부분)를 신뢰하는 것은 주의해야 한다. 또한, pathname만으로는 전체 URL의 컨텍스트를 파악하기 어려울 수 있으므로, 필요에 따라 location 객체의 다른 속성들과 함께 사용하는 것이 좋다.

## 라우터란?

라우터는 웹 애플리케이션에서 사용자가 다른 주소로 이동할 때마다 해당하는 페이지나 컴포넌트를 사용자에게 보여주는 기능을 담당한다. 주로 싱글 페이지 애플리케이션(SPA)에서 사용되며, 페이지를 새로 로딩하지 않고도 다양한 뷰를 제공할 수 있게 해준다.

## React Router

React Router는 React 애플리케이션에서 페이지 라우팅을 도와주는 라이브러리다. SPA에서 클라이언트 사이드 라우팅을 구현하여, 서버로부터 새로운 페이지를 가져오지 않고도 동적으로 컴포넌트를 변경할 수 있게 해준다.

```js
import { BrowserRouter, Route, Switch } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter> // 아래에서 설명
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="">
        <Route path="/users" element={<Users />} />
      </Routes>
    </BrowserRouter>
  );
}
```

## NavLink, Link, Navigate, useNavigate

### NavLink

NavLink 컴포넌트는 현재 경로와 매칭될 때 스타일이나 클래스를 자동으로 적용할 수 있는 Link의 특수한 형태다. 주로 네비게이션 링크에 한정되어 사용된다.

```jsx
<NavLink to="/about" activeClassName="active">
  About
</NavLink>
```

### Link

Link 컴포넌트는 애플리케이션 내에서 다른 경로로의 이동을 위해 사용된다. 페이지를 새로 로딩하지 않고 애플리케이션 내에서 라우팅을 할 수 있게 해준다.

```jsx
<Link to="/about">About</Link>
```

### Navigate & useNavigate

Navigate 컴포넌트와 useNavigate 훅은 프로그래매틱하게 다른 경로로 이동하고자 할 때 사용된다. useNavigate는 함수 컴포넌트 내에서 리디렉션을 위해 사용된다.사용자의 액션에 따라 다양한 조건으로 라우팅을 할 수 있다.

```jsx
function HomeButton() {
  let navigate = useNavigate();
  return (
    <button onClick={() => navigate('/home')}>
      Go Home
    </button>
  );
}
```

## RouterProvider

RouterProvider는 `React Router v6.4`에서 소개된 컴포넌트로, 애플리케이션의 라우팅 로직을 캡슐화한다. 새로운 라우팅 엔진을 사용하여 성능과 유연성을 향상시킨다. 애플리케이션의 루트 레벨에 위치하여 라우팅 컨텍스트를 제공하며, 앱 내 모든 라우팅이 이 컴포넌트를 통해 처리된다. 이전 버전의 React Router를 사용하던 프로젝트에서는 마이그레이션 과정이 필요할 수 있다.

```jsx
import { createBrowserRouter, RouterProvider } from 'react-router-dom';

const router = createBrowserRouter([
  {
    path: '/',
    element: <Home />,
  },
  {
    path: '/about',
    element: <About />,
  },
]);

function App() {
  return <RouterProvider router={router} />;
}
```

## Browser Router

`BrowserRouter`는 웹 애플리케이션의 URL을 HTML5 History API(푸시 상태와 팝 상태 이벤트)를 사용해 관리하는 라우터다. 이를 통해 페이지를 새로 고치지 않고도 주소를 변경할 수 있어, 사용자 경험을 크게 개선할 수 있다.

- 장점
  - 페이지 새로고침 없이 빠른 페이지 전환을 제공한다.
  - 검색 엔진이 페이지를 더 잘 이해할 수 있다.
- 단점:
  - 서버 측에서 모든 요청을 index.html로 리다이렉트하는 설정이 필요하다.

## Memory Router

`MemoryRouter`는 React Router의 하나로, 주로 테스트 환경이나 서버 사이드 렌더링에서 사용되며, 실제 URL을 변경하지 않고 라우팅을 시뮬레이션할 수 있다. 이는 Jest와 같은 테스트 프레임워크에서 React 컴포넌트의 라우팅 동작을 테스트할 때 매우 유용하다.

```jsx
import React from 'react';
import { render } from '@testing-library/react';
import { MemoryRouter } from 'react-router-dom';

function Home() {
  return <div>Home Page</div>;
}

function About() {
  return <div>About Page</div>;
}

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
      <Route path="">
      <Route path="/users" element={<Users />} />
    </Routes>
  );
}

describe('App Component Routing', () => {
  test('should render Home component for / route', () => {
    const { getByText } = render(
      <MemoryRouter initialEntries={['/']}>
        <App />
      </MemoryRouter>
    );
    expect(getByText('Home Page')).toBeInTheDocument();
  });

  test('should render About component for /about route', () => {
    const { getByText } = render(
      <MemoryRouter initialEntries={['/about']}>
        <App />
      </MemoryRouter>
    );
    expect(getByText('About Page')).toBeInTheDocument();
  });
});
```

## Web APIs - History

History API는 브라우저의 세션 히스토리에 접근하여, 현재 페이지를 새로고침하지 않고도 URL을 조작할 수 있는 웹 API다. 이 API를 사용하여 개발자는 복잡한 싱글 페이지 애플리케이션(SPA)의 라우팅 로직을 구현할 수 있다.

```js
// 현재 보고 있는 페이지를 새 URL로 대체
history.pushState({ page: 1 }, "title 1", "?page=1");
```

- 장점:
  - 페이지 새로고침 없이 URL을 변경할 수 있다.
  - 사용자가 브라우저의 뒤로 가기 버튼을 사용할 때 기대하는 동작을 구현할 수 있다.
- 단점:
  - 직접 History API를 사용할 때는 라우팅 로직을 세심하게 관리해야 한다.

> BrowserRouter vs MemoryRouter: BrowserRouter는 실제 브라우저 환경에서 사용되며, 사용자의 URL 변경을 통해 SPA 내에서의 페이지 전환을 처리한다. 반면, MemoryRouter는 메모리에 라우팅 정보를 저장하기 때문에, URL 변경 없이 테스트나 서버 사이드 렌더링 등의 환경에서 유용하게 사용된다.
> RouterProvider: React Router v6에서 도입된 이 컴포넌트는 새로운 라우팅 엔진과 함께 사용되어 더 나은 성능과 유연성을 제공한다. 기존의 <BrowserRouter> 등과 비교했을 때, 라우팅 구성이 더 간결하고 선언적이다.
> History API: 직접 History API를 사용하는 것은 라우터 라이브러리를 사용하는 것보다 더 많은 제어를 제공하지만, 복잡성이 증가하고 브라우저 호환성 문제를 직접 처리해야 한다는 단점이 있다. React Router와 같은 라이브러리는 이러한 복잡성을 추상화하여 개발자에게 간편한 인터페이스를 제공한다.
