# browser

## HTML Semantic Element

웹 표준을 중요하게 생각하자!

```html
<html>
  <body>
    <header></header>
    <main>
      <section>
        <article></article>
        <article></article>
      </section>
      <section>
        <ul>
          <li></li>
          <li></li>
        </ul>
        <ol>
          <li></li>
          <li></li>
        </ol>
      </section>
    </main>
    <footer></footer>
  </body>
</html>
```

## NodeList

- Node => 문서 내의 모든 객체
  - DOM에 접근할 때, array라고 생각하지 않는다.
- Element => Tag로 둘러싸인 요소

NodeList를 사용할때는 배열로 형변환하여 사용하면 array의 property를 사용할 수 있다. [...nodeList]

## innerHTML

굉장히 오래됐고, 좋지 않은 API (XSS 공격 위험, 속도도 매우 느림)

대체재: `insertAdjacentHTML`, `textContent` (문자열만 렌더링)

> [MDN (insertAdjacentHTML)](https://developer.mozilla.org/ko/docs/Web/API/Element/insertAdjacentHTML)
> [Can I use](https://caniuse.com/)

## Data Attributes

CSS에서도 접근이 가능하고, CSS 선택자에서도 접근이 가능하다.

```html
<html>
  <body>
    <main
      id='test'
      data-id='asdf'
      data-foo-bar='afa'
    >
    </main>
  </body>
  <script>
    const main = document.querySelector('main')

    console.log(main.dataset.fooBar) // 'afa'

    delete main.dataset.id // dataset 제거
  </script>
</html>
```

## Black Box Event Listener (주관)

### Black Box

  내부 구현이 어떻게 동작될지 예측할 수 없는 경우
  추상화가 너무 과하게 되거나 명시적인 코드가 아닌 경우

```js
const button = document.querySElector('button')

function getLog(e): void { // 명시적인 것이 좋음
  console.log(e);
}

// 버튼.이벤트_등록('이벤트_타입', 리스너_함수_실행) => 반응형으로 실행된다.
button.addEventListener('click', handleClick) // handleClick? 이해하기 어렵다.


// search bar
const handleClick = ():void => { // ❌ handleSearch라는 네이밍이 더 낫다.
  // 1. input을 받는 코드
  // 2. 유효성 검사를 하는 코드
  // 3. form을 전송하는 코드
}

button.addEventListener('click', handleClick) // ?...
```
