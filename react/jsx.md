# jsx

>jsx는 ECMAScript의 확장이다

❗️ `jsx`는 처음에 React와 함께 사용하기 위해 Meta(구 페이스북)에서 나왔지만, 다른 framework에서도 사용 가능하다

- vue, preact, solid.etc

변환기 중 제일 유명한 [Babel](https://babeljs.io/repl)로 확인 가능

→ `Presets`에서 `react`를 체크하거나, `Plugins`에서 `@babel/plugin-transform-react-jsx`를 추가하면 JSX를 실험 가능

JSX 파일에 /*@jsx foo*/ 주석을 추가하면 React.createElement 대신 `foo`를 쓰게 된다.

## React에서 JSX를 사용하는 목적

>React는 JSX 사용이 필수가 아니지만, 대부분의 사람은 JavaScript 코드 안에서 UI 관련 작업을 할 때 시각적으로 더 도움이 된다고 생각합니다. 또한 React가 더욱 도움이 되는 에러 및 경고 메시지를 표시할 수 있게 해줍니다.
>
>- [React 공식 문서](https://ko.legacy.reactjs.org/docs/introducing-jsx.html)

### JSX vs Pure Javascript

JSX 코드

```jsx
<div>
 <p>Count: {count}!</p>
 <button type="button" onClick={() => setCount(count + 1)}>Increase</button>
</div>
```

변환된 JS 코드

```jsx
React.createElement(
 "div",
 null,
 React.createElement("p", null, "Count: ", count, "!"),
 React.createElement("button", { type: "button", onClick: () => setCount(count + 1) }, "Increase")
);
```

## 컴포넌트를 생성하는 것은 최적화할 필요가 없다?

컴포넌트를 생성하는 비용은 매우 적기 때문에 리액트 공식 문서에서도 컴포넌트 생성 최적화를 할 필요는 없다고 언급되어 있다.

>Creating elements is extremely cheap so you don’t need to try to optimize or avoid it.
>
>- [React 공식 문서](https://react.dev/reference/react/createElement)

### 📎 Links

- [facebook의 JSX 소개](https://facebook.github.io/jsx/)
- [React 공식문서의 JSX 소개](https://ko.reactjs.org/docs/introducing-jsx.html)
- [Babel, JSX, 그리고 빌드 과정들](https://ko.reactjs.org/docs/faq-build.html)
- [JSX 이해하기](https://ko.reactjs.org/docs/jsx-in-depth.html)
