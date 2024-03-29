# react.md

## React 공식 문서

- [**React 공식문서**](https://ko.reactjs.org/)
- [**React Beta 문서**](https://beta.reactjs.org/)

### Rendering

- [createRoot](https://beta.reactjs.org/reference/react-dom/client/createRoot)
  - 한국어로 읽고 싶다면 [예전 문서](https://ko.reactjs.org/docs/react-dom-client.html#createroot)를 아주 살짝 참고하자.

여러 개의 Root를 만들거나, 여러 번 render해도 된다.
여러 번 render하는 카운터 예제

- [updating-a-root-component](https://beta.reactjs.org/reference/react-dom/client/createRoot#updating-a-root-component)

### Re-Rendering

- [React는 컴포넌트를 언제 다시 리렌더링 할까요?](https://velog.io/@surim014/react-rerender)
- [왜 리액트에서 리렌더링이 발생하는가](https://medium.com/@yujso66/%EB%B2%88%EC%97%AD-%EC%99%9C-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%97%90%EC%84%9C-%EB%A6%AC%EB%A0%8C%EB%8D%94%EB%A7%81%EC%9D%B4-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94%EA%B0%80-74dd239b0063)
- [React 렌더링 동작에 대한 (거의) 완벽한 가이드](https://velog.io/@superlipbalm/blogged-answers-a-mostly-complete-guide-to-react-rendering-behavior)

### Plus alpha

- [면접 때 종종 나오는 질문인 “React는 프레임워크인가요, 라이브러리인가요?”에 대한 React 개발자의 답변](https://twitter.com/trueadm/status/1194567962784653312)
- [제어의 역전](https://martinfowler.com/bliki/InversionOfControl.html)

> **'Ashal'** say:
>
>(IoC: Inversion of Control)이 Framework의 주요한 특징이고, React는 IoC를 통해 상태와 업데이트가 얽힌 복잡한 상황을 간단히 선언형 UI로 구성하는 혜택을 누린다(이게 바로 React의 첫 번째 특징이다). 그 누구도 매번 root를 render하는 방식으로 쓰면서 “이게 라이브러리지!”라며 감탄하지 않는다.
>
>하지만 일반적으로는 (Martin Fowler의 개탄처럼) IoC는 IoC 컨테이너와 엮여서 DI와 동의어처럼 쓰이고, Next.js, Remix 같은 걸 Framework이라고 부르니 면접 때 괜히 이런 걸로 싸우지는 말자. “리액트 개발자가 이렇게 이야기했다니까요!”라고 해봐야 서로 감정만 상할 뿐이다.
