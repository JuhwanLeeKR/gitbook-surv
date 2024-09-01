# react-environment-flow

## 생태계

- 대중성은 즉 개발로 바라본다면 생태계
- **오픈소스 생태계로 쌓인 맥락들과 지식은 무시할 수 없다.**
  - 사실 공부해보면 어이없는 이유도 있다.
- 생태계를 잘 알고 따르는 것은 당연히 차차 알아갈 수 있다.
- 무지성으로 따르느냐 그 맥락을 이해하냐의 차이가 개발자의 수준을 나타낸다.
- 이해하지 못한다면 `그냥 많이 쓰잖아요..`라는 답변을 내뱉을 수 있다.

## 2016

- 모바일 시장이 걷잡을 수 없이 커져갔다.
- 여전히 Spring + JSP + jQuery 조합이 강세
- 프론트엔드 프레임워크 대장은 AngularJS
- 해외에서는 Dan Abromov의 대활약
  - Redux
  - Hot Reloading
  - Time Trabel

## 2017

- AngularJS => Angular 넘어가는 학습이 많았다
- 하지만 대부분 TypeScript, RxJS 거부
- React 사용자와 사용 사례가 엄청나게 늘어남
- Redux 배우기 열풍
  - 하지만 대부분 Redux 조차 잘 못 다룸
  - Presentational & Container Components 대세로 자리매김
- jQuery 걷어내기 유행
- 하위 브라우저 호환 지옥

## 2018

- Angular vs React vs Vue 무한 논쟁
- React를 사용하거나 낮은 러닝커브의 Vue로 입문하자는 이야기가 자주 나옴
- 여전히 TypeScript에 대한 거부감이 심함
- Webpack, Babel 등 주변 도구 학습에 엄청난 고통을 느껴감
- React + Redux는 이미 공식 스펙에 가까워짐
- MobX의 등장으로 `Redux vs MobX` 논쟁이 많아짐
- 기술 역량이 괜찮은 경우 Redux Saga를 사용하는 사례가 점점 늘어남
- 다양한 하이브리드 앱에 수요가 서서히 증가

## 2019

- React는 완전한 대세로 자기매김
  - Vue도 나른 괜찮은 점유율을 가져감
- 수 많은 기업에서 TypeScript를 도입하기 시작
- styled-components 주도로 CSS in JS 사용 증가
- React v16.8 출시 (Hooks)
  - 함수형 프로그래밍 대유행 시작
- ContextAPI vs Redux
  - 상태관리에 대한 불신과 피로도에 대한 논쟁
  - GraphQL의 등장
- 프론트엔드 팀이 생겨나며 Prettier & ESLint & Husky & lint-staged 등 협업을 위한 고민과 해결 사례가 늘어나기 시작
- Vanilla JavaScript 학습 요구 대두
- 수 많은 라이브러리와 고급 프론트엔드 기법이 우수수 쏟아져나옴

## 2020

- React & Hooks API & TypeScript + Axios => 생태계 구축
  - React Native 사용 ㄱ업이 늘어감
- 3년 차 이상 프론트엔드 개발자 뽑는 것은 완전히 기본
  - Tree Shaking, Code Splitting, SSR, Hydration
- 대규모 FE 팀은 LErna를 주축으로 모노레포 노하우 쌓기 시작
- Recoil의 등장
- RTL & Jest를 주축으로 TDD에 대한 성숙도가 점점 올라감
- Storybook 사용 사례 증가
  - Atomic Design Pattern 도입 유행 + @headless UI
- Vue3 정식 출시 & Composition API 등장
  - 오히려 Vue => React 전환 케이스가 늘어나기 시작
- 뒤늦게 SEO 대응의 심각함을 깨우치기 시작
- 기업에서 성능 최적화를 요구하기 시작

## 2021

- 개발자 역대급 호황기
- AngularJS Deprecated
- React Query vs SWR => React Query 우위 점하는 중
- CI/CD & Github Actions & DX 등 프론트엔드 개발자의 영역 황장
- Storybook 활용도 증가 => 디자인시스템 & 디자인 토큰
- Figma 생태계 발전
- 성능 최적화는 당연한 수순으로 올라옴
- Zero Runtime CSS in JS 사용도 증가
- Redux Toolkit이 알려지기 시작했으나 정식 릴리즈도 안된 Recoil에 밀림
- Yarn Berry 사용도 급증
- Svelte를 사용하는 사례가 늘어나기 시작함
- Spring과 비슷한 NextJS 인기 급상승
- 토스의 기술 선도로 많은 프론트엔드 개발자들에게 동기부여
- 네카라쿠배와 국비교육으로 프론트엔드 개발 신입 급증

## 2022

- IT 대해고 시대 시작
- React v18 정식 릴리즈
- Next.js & TansStack Query 독주
- IE 지원 종료
- written by Rust 라이브러리 대유행 & WASM
- 무섭게 성장하는 Vercel
- Zustand (독일어) & Jotai (일본어)
  - Recoil은 대규모 해고 사건과 업데이트가 붕 뜨게 됨
- MFA (Micro Frontend Architecture)
- Lerna vs Turborepo vs NX vs Rush Stack
- Vite 도입에 엄청난 폭풍이 몰아침

## 2023

- 대규모 언어 모델(LLM) + 생성 AI
  - GPT에 충격받은 사람들 특히 개발자
  - 노코드 시대
- 전세계 경기 침체로 인한 IT 대해고 및 인력 효율화
- 5년차 이상 프론트엔드 개발자 뽑는 추세로 변화하는 추세
  - FE => TPM, TPO 직군 전환 움직임
- React Server Components
- 무섭게 성장하는 Vercel
- RSC에 더욱 진보된 렌더링 기법
  - ISR, Streaming SSR
- Qwik, Astro
  - like a React + React 호환 + 압도적인 퍼포먼스
- 특이한 흐름의 TypeScript 생태계
  - 강한 타입의 tRPC, Zod 열풍
- Recoil => Pmndrs
- CSS 스타일의 새로운 패러다임
