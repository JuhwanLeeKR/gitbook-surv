# error-handling

## 유효성 검사

사용자의 입력 값이 유효한지 확인하는 것
사용자와 상호작용 -> 사용자의 입력을 받거나 그것을 통해서 무언가 하게됩니다.

- 정규식
- JavaScript 문법
- 웹 표준 API

### 그럼 유효성 검사는 어디서 할까?

할 수 있는 모든 곳에서 다 처리하는 게 좋다.
사용자의 입력 => 클라이언트 (HTML, Javascript) => 백엔드에서도 처리

## try ~ catch

### 왜 예외를 처리하는가?

프론트엔드 (클라이언트) 측에서는 사용자의 입력을 받는다!

개발자가, 프로그래머가, 모든 에러를 예측하여 처리하기가 어렵고 거의 불가능하다

```js

function handleSubmit(input) {
  // - 중요하지 않다고 생각하는 핸들링도 제외하면 안된다. => 모든 logic을 try catch에 넣는다.
  // - try catch 안에 try catch를 또 사용하지 않고, 함수 단위로 사용한다.
  try {
  // 예외가 예상되는 코드 혹은 발생시킬 코드
  } catch (error) {
    /**
     예외를 처리하는 코드
     1. 개발자를 위한 예외처리 => 동료 개발자에게 제안을
     console.warn(error) console.error(error)

     2. 사용자를 위한 예외처리 => 사용자가 볼 수 있다고 생각
     alert(err) ❌
     alert('404 Not found') ❌
     alert('잠시만 기다려주세요, 어떤 문제가 있습니다 다시 시도해 주세요') ✅

     3. 사용자에게 사용을 제안
     history.back()
     history.go('안전한 어딘가로..')
     clear()
     element.focus()

     4. 에러 로그 수집
     sentry.전송()

     5. 비추천하지만 필요에 따라 사용되는 경우
     handleSubmit() // 재귀
     */
  } finally {
    // 데이터 분석을 위한 로그를 넣는 편
  }
}
```

## 사용자에게 알려주기

- 동료 개발자
- 내가 만든 앱을 이용하는 사용자
  - 내가 만든 라이브러리 => e.g) React
  - 내가 만든 실제 앱 => e.g) 간단한 애플리케이션, 계산기

```js
const const = 'hello' // ❌

console.log(hello) // ❌
const hello = 'hello'


function React() {
  // 생성자로 사용하길 바랄때...!
  if (!new.target) {
    throw new ReferenceError('생성자입니다!!')
  }
}

React() // ReferenceError:생성자입니다!!
```
