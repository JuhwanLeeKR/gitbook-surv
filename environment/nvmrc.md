# .nvmrc 파일 작성 가이드

`.nvmrc` 파일은 프로젝트의 루트 디렉토리에 위치해야 하며, 사용하려는 Node.js의 버전을 지정합니다. 이 파일은 단순한 텍스트 파일이므로, 텍스트 에디터를 사용하여 작성할 수 있습니다.
다음은 `.nvmrc` 파일의 다양한 작성 방법입니다.

## 특정 버전 지정하기

특정 버전의 Node.js를 사용하려면, 해당 버전 번호를 `.nvmrc` 파일에 작성합니다.

```zsh
v18.17.0 # Node.js 18.17.0 버전을 사용
```

## 메이저 버전 지정하기

특정 메이저 버전의 최신 버전을 사용하려면, 메이저 버전 번호만을 작성합니다.

```zsh
20 # Node.js 20.x의 최신 버전을 사용
```

## 버전 범위 지정하기

버전 범위를 지정하려면, 해당 범위를 기술합니다.

```zsh
>=16.0.0 # 16.0.0 이상의 Node.js 버전이 사용
```

## LTS 버전 사용하기

가장 최신의 LTS(Long Term Support) 버전을 사용하려면, `lts/*`를 사용합니다.

```zsh
lts/* # 가장 최신의 LTS 버전을 사용
```

## 최신 버전 사용하기

가장 최신 버전의 Node.js를 사용하려면, `node`를 작성합니다.

```zsh
node # 가장 최신 버전의 Node.js가 사용
```

***

- `fnm`을 사용하는 경우 자동으로 fnm이 `.nvmrc` 파일을 읽고 버전 설정을 해줍니다.
- `nvm`을 사용하는 경우 해당 디렉토리에서 `nvm use` 명령을 실행하면 `nvm`이 해당 파일을 읽고 지정된 버전의 Node.js를 사용하게 됩니다.