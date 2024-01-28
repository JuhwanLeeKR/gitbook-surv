# typescript

## REPL (Read-Eval(Evaluation)-Print Loop)

사용자가 코드를 입력하면 입력한 코드를 평가하고 코드의 실행결과를 출력해주는 것을 반복해주는 환경

- Using **with Typescript**

```zsh
npx ts-node # 실행

Ctrl + C or .exit # 종료
```

## 타입 지정하기 (Simple examples)

- [Typescript 공식 문서](https://www.typescriptlang.org/) 읽는 것을 더 추천한다

```ts
let name: string;
let age: number;

name = '홍길동'; // 🆗
age = 13; // 🆗

name = 13; // ❌
age = '홍길동'; // ❌

let human: {
  name: string;
  age: number;
};

human = { name: '홍길동', age: 13 };
```

### Generics, Utility Types, and Tips

- [Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html)
- [Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)
- [더 좋은 타입스크립트 프로그래머로 만드는 11가지 팁](https://velog.io/@lky5697/11-tips-that-help-you-become-a-better-typescript-programmer)

오래된 라이브러리의 경우 d.ts 파일만 따로 패키지로 제공된다. 패키지 이름은 `@types/foo` 형태.

- [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)
- [DefinitelyTyped/types](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/types)

- [DefinitelyTyped/types/react](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/types/react)
