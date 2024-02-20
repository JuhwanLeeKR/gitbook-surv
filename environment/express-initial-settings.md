# express

## express란?

- [Node.js를 위한 빠르고 개방적인 간결한 웹 프레임 워크](https://expressjs.com/ko/)
- Node.js 초창기부터 존재하던 프레임워크

<!--
- Express 란
- URL 구조
- REST API
  대개는 “필딩 제약 조건” 4가지를 모두 만족하지 않고, Resource와 HTTP Verb만 도입하는 수준으로 사용.

- 이렇게 안 하고: /write-post
- 이렇게 하자: /posts → 뭔가를 한다 (CRUD)

CRUD에 대해 HTTP Method를 대입. Read는 Collection(복수)과 Item(Element)(단수)로 나뉨.

기본 리소스 URL: /products

1. Read (Collection) → GET /products ⇒ 상품 목록 확인
2. Read (Item) → GET /products/{id} ⇒ 특정 상품 정보 확인
3. Create (Collection Pattern 활용) → POST /products ⇒ 상품 추가 (JSON 정보 함께 전달)
4. Update (Item) → PUT 또는 PATCH /products/{id} ⇒ 특정 상품 정보 변경 (JSON 정보 함께 전달)
5. Delete (Item) → DELETE /products/{id} ⇒ 특정 상품 삭제

- HTTP Method(CRUD)

 -->

## 초기 세팅 구성하기

### 1. 폴더 생성, 패키지 초기화, `.gitignore` 생성

```bash
mkdir express-demo-app
cd mkdir express-demo-app
```

```bash
npm init -y
```

```bash
touch .gitignore
echo "/node_modules/" > .gitignore # 내용 작성
```

### 2. Typescript, ESLint, ts-node, Express 설치

TypeScript

```bash
npm i -D typescript
npx tsc --init

npm i -D eslint

npm i -D ts-node

npm i express
npm i -D @types/express
```

```bash
npx eslint --init
```

- eslint 설정 예시

```bash
✔ How would you like to use ESLint? · style
✔ What type of modules does your project use? · esm
✔ Which framework does your project use? · none
✔ Does your project use TypeScript? · No / Yes
✔ Where does your code run? · node
✔ How would you like to define a style for your project? · guide
✔ Which style guide do you want to follow? · xo-typescript
✔ What format do you want your config file to be in? · JavaScript
```

### 3. nodemon 설치 및 `package.json` 수정

```bash
npm i -D nodemon
```

```json
{
 ...
 "scripts": {
  "start": "nodemon app.ts",
  ...
 },
 ...
}

```

### 4. CORS를 위한 [CORS 미들웨어](https://expressjs.com/en/resources/middleware/cors.html) 설치

```bash
npm i cors
npm i -D @types/cors
```

- 미들웨어 사용

```ts
import express from 'express';
import cors from 'cors';

const app = express();

app.use(cors());
```
