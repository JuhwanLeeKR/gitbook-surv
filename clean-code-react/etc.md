# etc

## import react

v17 부터 `import React from 'react'` 코드를 넣을 필요 없다.

큰 이득은 없으나, 불필요한 코드라인이 사라진다. (실제로 성능 개선 효과가 조금 있다)

## 디렉터리 구조

정답은 없지만 `의존성 덩어리` 그 자체이다.

- Prefix 단위로 컴포넌트로 구분해보자 (결합도)
- 하나의 onDepth만으로 표현할 수 있다. (depth가 깊어지기 전까지 파일명으로 구분하는 것이 나을 수 있다)
- 하나하나 점진적으로 늘려가는 것도 방법이다!

디렉토리 구조에 정답은 없다!

프로젝트 규모에 따라 계속 바꿔나가는 것도 좋은 방법!

## SPA에서의 새로고침

- `window.location.reload()` : SPA 입장에서는 특히나 앱을 완정히 종료하고 다시 실행하는 행위이다
  - 성능 저하, 상태 손실, 불필요한 서버 요청 등의 문제가 발생할 수 있음.

## Primitive UI

- 도메인 네임보다는
  - Sematic한 Primitive UI를 묘사한다.
    - RadixUI, ChakraUI
  - 생김새를 묘사한다.
    - Box, Circle, List, Square
