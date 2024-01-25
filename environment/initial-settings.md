# Initial-settings

## TypeScript + React + Jest + ESLint + Parcel 개발 환경 설정

1. 폴더 생성 및 패키지 생성

   ```zsh
   mkdir project-init

   cd project-init
   ```

   ```zsh
   npm init -y
   ```

2. `.gitignore` 파일을 작성

   ```zsh
   touch .gitignore
   ```

   [gitignore.io](https://www.toptal.com/developers/gitignore)

3. 타입스크립트 설정

   ```zsh
   npm i -D typescript

   npx tsc --init
   ```

4. `tsconfig.json` 파일 수정

   ```json
   {
     "compilerOptions": {
       ...
       "jsx": "react-jsx"
       ...
     },
     // 추후에 설치할 jest와 eslint를 위해 우선 작성
     "include": ["./jest-setup.ts", "./.eslintrc.js", "src/**/*"],
     "exclude": ["node_modules", "build", "dist"]
   }
   ```

5. ESLint 설정

   ```zsh
   npm i -D eslint

   npx eslint --init
   ```

6. `.eslintrc.js` 파일 수정

   ```js
   module.exports = {
   	env: {
   		browser: true,
   		es2021: true,
   		// jest 설치 전 미리 세팅
   		jest: true,
   	},
   	extends: [
   		'xo',
   		'plugin:react/recommended',
   		'plugin:react/jsx-runtime',
   		'prettier',
   	],
   	overrides: [
   		{
   			env: {
   				node: true,
   			},
   			files: ['.eslintrc.{js,cjs}'],
   			parserOptions: {
   				sourceType: 'script',
   			},
   		},
   		{
   			extends: ['xo-typescript'],
   			files: ['*.ts', '*.tsx'],
   		},
   	],
   	parserOptions: {
   		ecmaVersion: 'latest',
   		sourceType: 'module',
   	},
   	plugins: ['react'],
   	rules: {},
   	settings: {
   		react: {
   			version: 'detect',
   		},
   	},
   };
   ```

7. `.eslintignore` 파일을 작성

   `.gitignore` 파일 내용과 일치해도 무방

8. 리액트 설치

   ```zsh
   npm i react react-dom

   npm i -D @types/react @types/react-dom
   ```

9. 테스팅 도구 설치

```zsh
npm i -D jest @types/jest @swc/core @swc/jest \
    jest-environment-jsdom \
    @testing-library/react @testing-library/jest-dom
```

10. `jest-setup.ts` 파일 생성

    ```ts
    import '@testing-library/jest-dom';
    ```

11. `jest.config.js` 파일을 작성해 테스트에서 SWC를 사용

    ```js
    module.exports = {
    	testEnvironment: 'jsdom',
    	setupFilesAfterEnv: [
    		'@testing-library/jest-dom/extend-expect',
    		'./jest.setup',
    	],
    	transform: {
    		'^.+\\.(t|j)sx?$': [
    			'@swc/jest',
    			{
    				jsc: {
    					parser: {
    						syntax: 'typescript',
    						jsx: true,
    						decorators: true,
    					},
    					transform: {
    						react: {
    							runtime: 'automatic',
    						},
    					},
    				},
    			},
    		],
    	},
    	testPathIgnorePatterns: ['<rootDir>/node_modules/', '<rootDir>/dist/'],
    };
    ```

12. Parcel 설치

    ```zsh
    npm i -D parcel
    ```

13. `package.json` 파일의 scripts를 적절히 수정한다.

    ```json
    ...
    "scripts": {
      "start": "parcel --port 8080",
      "build": "parcel build",
      "check": "tsc --noEmit",
      "lint": "eslint --fix --ext .js,.jsx,.ts,.tsx .",
      "test": "jest",
      "coverage": "jest --coverage --coverage-reporters html",
      "watch:test": "jest --watchAll"
    },
    ...
    ```

14. 기본 코드 추가
    - `index.html`
    - `src/main.tsx`
    - `src/App.tsx`
    - `src/App.test.tsx`
    - `src/components/Greeting.test.tsx`
    - `src/components/Greeting.tsx`

### 기타 링크

- [**fnm (Fast Node Manager)**](https://fnm.vercel.app/)
