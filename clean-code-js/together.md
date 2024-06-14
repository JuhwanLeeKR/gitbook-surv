# together

## 공백

공백도 **코드 작성의 일부**다.

```js

// 1. 선언
// 2. 로직, 문
// 3. 반환
// 순으로 함수를 짜면 좋다.
// eslint padding-line-between-statements 사용 추천

```

## indent depth

: 복잡해 질수록 깊어진다!

HTML: 2 depth
JS: 2, 4 depth

### 깊어지는 depth 해결하는 법

- 의식적으로 코드를 작성

1. early return
2. callback => Promise => Async & Await
3. 고차 함수 (map, reduce, filter)
4. 함수를 나누고 추상화하기
5. 메서드 체이닝 (.then().then().then())

- 도구를 사용해서 통일

## 스타일 가이드

네이밍 컨벤션을 포함하는 규칙을 위한 가이드라인으로 하나의 팀 혹은 집단을 위해 존재, 즉 협업에 큰 도움을 주기 위함

- 서로를 이해하기 위한 시간 절약
- 코드 품질
- 일관성
- 가독성 향상
- 유지보수 용이성

> [Redux Style Guide](https://redux.js.org/style-guide/)
> [Rushstack Style Guide](https://github.com/microsoft/rushstack)
> [우리 팀을 위한 ESLint, Prettier 공유 컨피그 만들어보기](https://techblog.woowahan.com/15903/)
