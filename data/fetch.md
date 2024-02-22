# fetch

## Fetch API란?

`Fetch API`는 브라우저에서 서버로 네트워크 요청을 보내고 받기 위한 현대적인 인터페이스이다. `XMLHttpRequest(XHR)`의 보다 간단하고 유연한 대안으로, `Promise` 기반으로 작동하여 비동기 네트워크 통신을 쉽게 처리할 수 있다. Fetch API를 사용하면 리소스를 네트워크에서 쉽게 가져올 수 있으며, 요청과 응답을 조작하는 기능도 포함한다.

```js
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

## Promise

`Promise`는 비동기 작업의 최종 완료(또는 실패) 및 그 결과값을 나타내는 객체이다. 콜백 함수의 연쇄적인 호출 대신, 비동기 작업을 보다 쉽게 처리할 수 있게 해주며, .then(), .catch(), .finally() 메소드를 통해 성공, 실패, 완료 시 실행할 로직을 지정할 수 있다.

```js
const myPromise = new Promise((resolve, reject) => {
  const condition = true;
  if (condition) {
    resolve('Promise is resolved successfully.');
  } else {
    reject('Promise is rejected.');
  }
});

myPromise
  .then(result => console.log(result))
  .catch(error => console.error(error));
```

## ReadableStream

`ReadableStream`은 데이터를 조각별로 읽을 수 있는 스트림 인터페이스다. 웹에서는 이를 통해 대용량 데이터를 조각으로 나누어 점진적으로 처리할 수 있으며, 이는 네트워크 응답이나 파일 읽기 같은 I/O 작업에서 특히 유용하다.

예를 들어, 큰 파일을 다운로드하거나 비디오를 스트리밍할 때, 전체 데이터를 한 번에 로드하는 대신에 ReadableStream을 사용하여 데이터의 일부분만 메모리에 로드하고 처리할 수 있다. 이 방식은 메모리 사용량을 줄이고, 사용자에게 더 빠른 인터랙션을 제공할 수 있게 해준다.

```js
async function fetchAndProcessStream(url) {
  // Fetch API를 사용하여 리소스 요청
  const response = await fetch(url);

  // 응답 본문을 ReadableStream으로 받음
  const reader = response.body.getReader();

  // 스트림을 처리하는 함수
  async function processStream() {
    const { done, value } = await reader.read(); // 스트림에서 데이터 조각(청크)을 읽음
    if (done) {
      console.log('Stream processing completed');
      return;
    }

    // 여기에서 데이터 조각(value)을 처리 (예: 화면에 표시)
    console.log(value);

    // 재귀적으로 함수를 호출하여 스트림의 나머지 부분을 계속 읽음
    await processStream();
  }

  // 스트림 처리 시작
  await processStream();
}
```

## 아스키코드(ASCII)와 유니코드(Unicode)

### 아스키코드(ASCII)

아스키코드는 1960년대에 개발된 7비트 인코딩 체계로, 주로 영문 알파벳을 표현하기 위해 설계되었다.
0부터 127까지의 숫자를 사용하여 128개의 문자를 표현한다. 이에는 영문 대소문자, 숫자, 특수문자 등이 포함된다.

아스키코드는 영어와 기본적인 특수문자만을 지원하기 때문에 다른 언어를 표현하는 데에는 한계가 있다. 특히, 한글과 같은 비영어권 문자를 표현할 수 없다.

### 유니코드(Unicode)

유니코드는 전 세계의 모든 문자를 하나의 일관된 문자 세트로 표현하기 위해 개발된 국제 표준 인코딩 체계이다.
현재 수십만 개의 문자를 포함하고 있으며, 이는 계속 확장되고 있다. 유니코드는 여러 언어의 문자, 기호, 이모티콘 등을 포함한다.
유니코드는 다양한 언어와 기호를 하나의 통합된 체계에서 지원하기 때문에 글로벌한 커뮤니케이션과 데이터 교환에 있어 중요한 역할을 한다.

#### 한국어에서 `안녕하세요`라는 표현을 살펴보자

- 아스키코드: 아스키코드로는 한국어 문자를 직접 표현할 수 없다. 따라서, 한국어를 처리하기 위해서는 `EUC-KR`이나 `CP949`와 같은 확장 인코딩 체계를 사용해야 한다. 이는 아스키코드를 기반으로 하면서 추가 바이트를 사용하여 한국어를 포함한 다른 문자를 표현한다.
- 유니코드: 유니코드에서는 `안녕하세요`를 각 글자에 해당하는 고유한 코드 포인트로 표현한다. 예를 들어, "안"은 `U+548C`, "녕"은 `U+60A9` 같이 유니코드 포인트를 사용하여 표현된다. 유니코드의 도입으로 인해, 다양한 언어의 문자가 하나의 문서에서도 자유롭게 혼용될 수 있게 되었다. 이는 웹 개발, 소프트웨어 개발, 데이터 저장 및 교환 등 다양한 분야에서 글로벌 호환성을 제공한다.

아스키코드와 유니코드의 가장 큰 차이는 **지원하는 문자 범위**와 **글로벌 호환성**에 있다. 유니코드는 세계의 모든 문자 체계를 포괄하는 광범위한 인코딩 체계를 제공함으로써, 다국어 환경에서의 커뮤니케이션과 데이터 처리의 표준이 되었다.

>**참고 링크**
>
>- [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
>- [Streams API](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API)
>- [Using Readable Streams](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API/Using_readable_streams)
>- [아스키코드](https://ko.wikipedia.org/wiki/ASCII)
>- [유니코드](https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%88%EC%BD%94%EB%93%9C)
