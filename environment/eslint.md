# eslint

## [**ESLint 공식문서**](https://eslint.org/)

- 스타일 통일
- 잠재적 문제 발견
- 베스트 프랙티스 추천 → 최신 트렌드를 학습하는데 활용할 수 있다.

- [린트](https://ko.wikipedia.org/wiki/린트_(소프트웨어))
- [정적 프로그램 분석](https://ko.wikipedia.org/wiki/정적_프로그램_분석)
- [Coding_conventions](https://en.wikipedia.org/wiki/Coding_conventions)

## Only ESLint vs ESLint + prettier (Result of asking ChatGPT)

### ESLint만 사용할 때

#### 장점 (Only ESLint)

- **통합 관리**: 코드의 스타일과 버그를 한 도구로 관리할 수 있어 관리가 간편합니다.
- **구성 유연성**: ESLint는 코드 품질과 스타일 관련 규칙 모두를 설정할 수 있어, 사용자의 필요에 맞게 세부적인 조정이 가능합니다.

#### 단점 (Only ESLint)

- **설정 복잡성**: 스타일 규칙을 모두 직접 설정해야 하므로 설정이 복잡해질 수 있습니다.
- **제한된 스타일링 옵션**: ESLint는 주로 코드 품질과 문제점에 중점을 두고 있으며, Prettier만큼 다양한 스타일링 옵션을 제공하지 않을 수 있습니다.

### ESLint와 Prettier 함께 사용할 때

#### 장점 (ESLint + prettier)

- **최적화된 스타일링**: Prettier는 코드 스타일링에 특화되어 있어 일관된 코드 스타일을 유지할 수 있습니다.
- **자동화된 포맷팅**: Prettier는 코드를 자동으로 포맷팅해주어 개발자가 수동으로 스타일을 관리하는 데 드는 시간을 줄여줍니다.
- **명확한 역할 분담**: ESLint는 코드 품질과 관련된 문제에 집중하고, Prettier는 스타일링에 집중합니다. 이로 인해 각 도구의 역할이 명확해져 효율적으로 작업할 수 있습니다.

#### 단점 (ESLint + prettier)

- **설정 복잡성 증가**: 두 도구 모두를 설정하고 관리해야 하므로 초기 설정이 복잡해질 수 있습니다.
- **통합 문제**: 때때로 ESLint의 규칙과 Prettier의 포맷팅이 충돌할 수 있으며, 이를 해결하기 위해 추가적인 통합 작업이 필요할 수 있습니다.

### 결론

- **ESLint만 사용**: 간단한 프로젝트나 특정한 스타일 규칙에 대한 세밀한 컨트롤이 필요한 경우 적합합니다.
- **ESLint와 Prettier 함께 사용**: 대규모 프로젝트나 팀 작업에서 일관된 코드 스타일을 유지하고자 할 때 좋은 선택입니다.

### Tips: Ashal' VS Code common setting

- [VS Code 기본 세팅](https://github.com/ahastudio/CodingLife/blob/main/20211008/react/.vscode/settings.json)
- [Trailing Spaces](https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces)
