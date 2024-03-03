# MSW(Mock Service Worker)

<!--
MSW keyword
- Service worker
- MSW(Mock Service Worker)
- polyfill(폴리필)
 -->

## [MSW(Mock Service Worker)](https://v1.mswjs.io/)란?

코드 레벨이 아니라 네트워크 레벨에서 가짜 구현을 해주는 것. 오프라인 작업 등을 지원하기 위한 [Service worker](https://developer.mozilla.org/ko/docs/Web/API/Service_Worker_API)의 기능을 유용히 활용한 것

### 1. MSW 패키지 설치

MSW 2.0 이전의 버전을 다루고 있으니, 최근에 업데이트 된 2.0 버전과 사용법이 다를 수 있습니다.

```bash
npm i -D msw # msw@0.36.4
```

### 2. setupTests.ts 생성

```bash
touch src/setupTests.ts
```

jest.config.js 파일의 "setupFilesAfterEnv" 속성에 setupTests.ts 파일 추가

```js
module.export = {
  ...
  setupFilesAfterEnv: [
    ...,
    '<rootDir>/src/setupTests.ts',
  ],
 ...
}
```

TODO: msw 2버전 이상 사용법으로 구성하여 다시 작성

## Polyfill (폴리필)
