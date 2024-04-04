# week-8

## 반응형 웹 디자인(Responsive web design)

반응형 웹 디자인은 웹사이트가 다양한 화면 크기와 장치에 자동으로 최적화되게 하는 접근 방식이다. 핵심은 사용자가 어떤 장치를 사용하든 간에, 웹사이트가 효과적으로 작동하고 최적의 사용자 경험을 제공해야 한다는 것이다. 이를 위해 CSS 미디어 쿼리, 유연한 그리드 기반 레이아웃, 유연한 이미지와 같은 기술이 활용된다. 예를 들어, 스마트폰, 태블릿, 데스크탑 컴퓨터에서 동일한 웹사이트를 열 때, 레이아웃은 각 장치의 화면 크기에 맞춰 자동으로 조정된다. 이렇게 하면 개발자는 다양한 장치용으로 별도의 웹사이트를 만들 필요 없이, 단일 웹사이트로 다양한 화면 크기와 해상도를 커버할 수 있다.

## 디자인 시스템(Design System)

디자인 시스템은 제품이나 서비스의 디자인을 통일, 일관성 있게 관리하기 위한 일련의 표준화된 원칙, 규칙, 제약사항을 의미한다. 컴포넌트(재사용 가능한 디자인 요소), 패턴(디자인 문제를 해결하기 위한 검증된 해결책), 스타일 가이드(색상, 글꼴, 아이콘 등의 디자인 지침)로 구성된다. 대규모 팀에서 일관된 사용자 경험을 제공하고, 효율적인 협업과 빠른 제품 개발을 가능하게 한다. 예를 들어, 대형 기업의 웹사이트와 애플리케이션은 수많은 페이지와 기능으로 구성되어 있는데, 디자인 시스템을 통해 모든 제품에서 일관된 룩앤필을 유지할 수 있다.

## Atomic Design

Atomic Design은 인터페이스를 구축하기 위한 방법론으로, 원자(Atoms), 분자(Molecules), 유기체(Organisms), 템플릿(Templates), 페이지(Pages)의 다섯 가지 단계로 구성된다. 이 방법론은 웹사이트나 앱을 작은 단위로 분해하고, 이를 조합하여 복잡한 인터페이스를 구축하는 과정을 체계화한다. 원자는 가장 작은 단위(예: 버튼, 인풋)로, 분자는 원자들을 결합하여 더 구체적인 기능을 하는 단위(예: 검색 폼)로 구성된다. 유기체는 분자들이 모여 더 큰 섹션을 형성한다(예: 헤더).
템플릿은 유기체와 다른 컴포넌트들을 통해 페이지의 구조를 정의하며, 페이지는 템플릿에 실제 내용을 채워넣어 사용자에게 보여지는 최종 결과물이다. Atomic Design은 디자인과 개발 과정에서의 일관성과 재사용성을 높이며, 복잡한 인터페이스도 체계적으로 관리할 수 있게 한다.

## className

className은 HTML에서 CSS 클래스를 지정할 때 사용하는 속성이다. React 같은 JavaScript 라이브러리에서는 HTML 속성인 class 대신 className을 사용하여 DOM 요소의 클래스를 지정한다. 이는 JavaScript에서 class가 예약어로 사용되기 때문이다.

### HTML에서 className 사용하기

HTML에서 클래스를 추가하려면 class 속성을 사용한다.

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .red-text {
            color: red;
        }
    </style>
</head>
<body>

    <h1 class="red-text">이 텍스트는 빨간색으로 표시된다.</h1>

</body>
</html>
```

### React에서 className 사용하기

React 컴포넌트에서는 className 속성을 사용하여 클래스를 지정한다.

```jsx
import React from 'react';
import './App.css'; // CSS 파일 임포트

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <p>
          React에서 <code>className</code>을 사용해 스타일을 적용할 수 있다.
        </p>
      </header>
    </div>
  );
}

export default App;
```

```css
.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}
```

## 의미있는 마크업

의미있는 마크업은 웹 페이지의 내용과 구조를 정확히 전달하기 위해 적절한 HTML 요소를 사용하는 것을 말한다.
이 방식은 웹 접근성과 검색 엔진 최적화(SEO)를 향상시키며, 코드의 가독성과 유지 보수성을 높인다. 예를 들어, 기사의 제목에는 `<h1>` 태그를, 단락에는 `<p>` 태그를, 중요한 키워드에는 `<strong>` 태그를 사용하는 것이 의미있는 마크업의 예이다. 의미있는 마크업을 사용함으로써, 웹 페이지의 구조를 명확히 하고, 사용자와 검색 엔진 모두에게 콘텐츠의 의미를 더 잘 전달할 수 있다.

## CSS in JS 란?

CSS in JS는 JavaScript를 사용하여 스타일을 구성하고 적용하는 기법이다. 이 접근 방식은 컴포넌트 기반의 개발 방식, 특히 React와 같은 현대적인 JavaScript 프레임워크와 잘 어울린다. CSS in JS를 사용하면, 스타일 시트를 별도로 관리하는 대신 JavaScript 파일 내에 스타일을 직접 포함시킬 수 있어, 컴포넌트의 로직과 스타일이 한 곳에 모여 있게 된다. 이로 인해 컴포넌트의 재사용성과 유지 보수성이 향상된다.
CSS in JS에는 styled-components, emotion 등 여러 라이브러리가 있으며, 이들은 동적 스타일링, 서버 사이드 렌더링 지원 등 다양한 기능을 제공한다.

## CSS

CSS(Cascading Style Sheets)는 요소가 화면, 종이, 음성 또는 기타 미디어에 표시되는 방식을 포함하여 HTML 또는 XML로 작성된 문서의 표시를 지시하는 데 사용되는 스타일시트 언어이다. 웹 개발의 초석으로, 웹 페이지 디자인을 콘텐츠와 분리할 수 있으므로 레이아웃, 색상, 글꼴과 같은 요소의 스타일을 여러 웹 페이지에서 일관되게 지정할 수 있다. CSS를 사용하면 개발자는 웹 페이지의 시각적 측면을 제어하여 웹을 시각적으로 더욱 다양하고 매력적인 환경으로 만들 수 있다.

## styled-components

`styled-components`는 React와 같은 컴포넌트 기반 프레임워크에서 사용하기 위해 설계된 CSS-in-JS 라이브러리이다. 이 라이브러리를 사용하면 JavaScript 파일 내부에서 CSS를 정의할 수 있어 스타일과 컴포넌트가 밀접하게 결합된다. 이 방식은 스타일 시트가 분리되어 있을 때 발생할 수 있는 여러 문제를 해결해 준다.

- 컴포넌트 기반 스타일링: 각 컴포넌트의 스타일을 캡슐화하여 다른 컴포넌트의 스타일에 영향을 받지 않는다.
- 실시간 스타일 변경: props 또는 global theme을 기반으로 동적으로 스타일을 변경할 수 있다.
- 유지 관리 용이: 스타일을 별도의 파일로 분리하지 않고 컴포넌트 내부에 정의하기 때문에, 컴포넌트와 스타일이 한 곳에 있어 관리가 용이하다.
- 자동 벤더 프리픽스 적용: 스타일을 자동으로 처리하여 크로스 브라우징 이슈를 최소화한다.
- 서버 사이드 렌더링 지원: SEO 최적화를 위해 서버 사이드 렌더링을 지원한다.

```jsx
import styled from 'styled-components';

const StyledButton = styled.button`
  background-color: ${(props) => props.primary ? 'blue' : 'white'};
  color: ${(props) => props.primary ? 'white' : 'blue'};
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid blue;
  border-radius: 3px;

  &:hover {
    background-color: ${(props) => props.primary ? 'darkblue' : 'lightblue'};
  }
`;

function App() {
  return (
    <div>
      <StyledButton primary>Primary Button</StyledButton>
      <StyledButton>Secondary Button</StyledButton>
    </div>
  );
}

export default App;
```

## props

웹 개발의 맥락에서, 특히 React와 같은 프레임워크 내에서 `props`는 속성의 약자이다. 이는 상위 구성 요소에서 하위 구성 요소로 데이터를 전달하는 방법으로, 구성 요소가 사용될 때 구성 요소의 속성을 동적으로 설정할 수 있다. 이 메커니즘은 React의 컴포넌트 기반 아키텍처의 핵심으로, 동일한 컴포넌트 유형에 다양한 데이터를 전달하여 더 동적이고 재사용 가능한 컴포넌트를 허용하고 제공된 props에 따라 모양이나 동작을 사용자 정의한다.

## attrs

styled-components의 `attrs` 메서드는 컴포넌트에 속성을 미리 정의하는 데 사용된다. 이 기능을 사용하면 컴포넌트에 기본 속성을 설정하거나, 속성을 동적으로 계산하여 컴포넌트에 전달할 수 있다. `attrs`는 컴포넌트의 재사용성과 가독성을 높이는 데 도움을 준다.

`attrs` 메서드는 객체 형식으로 속성을 정의하며, 이 객체 내에서는 정적 값 또는 함수를 사용할 수 있다.
함수를 사용할 경우, 컴포넌트의 props를 인자로 받아 동적으로 속성 값을 결정할 수 있다.

```jsx
import styled from 'styled-components';

const Input = styled.input.attrs(props => ({
  type: "text",
  size: props.size || "1em",
}))`
  border: 2px solid palevioletred;
  margin: ${props => props.size};
  padding: ${props => props.size};
`;

function App() {
  return <Input size="2em" />;
}
```

```jsx
const Button = styled.button.attrs(props => ({
  // 동적으로 속성 값을 계산
  disabled: props.loading,
}))`
  background: ${props => (props.loading ? "gray" : "blue")};
  color: white;
  cursor: ${props => (props.loading ? "not-allowed" : "pointer")};
`;

function App() {
  return <Button loading={true}>Load Data</Button>;
}
```

`attrs`를 사용할 때는 컴포넌트의 props에 의존하는 속성 값들이 예상대로 동작하는지 확인해야 한다. 동적 속성은 컴포넌트의 외부 상태나 props에 따라 변할 수 있으므로, 컴포넌트의 반응성과 재사용성을 고려하여 설계해야 한다.

`attrs`는 컴포넌트에 기본적으로 적용되어야 하는 속성이나, 여러 컴포넌트에 걸쳐 일관적으로 사용되어야 하는 속성을 정의할 때 특히 유용하다. 이 메서드를 사용함으로써, 컴포넌트의 선언적 정의를 강화하고, 코드의 재사용성과 가독성을 높일 수 있다.

## Reset CSS

`Reset CSS`는 요소에서 모든 기본 브라우저 스타일을 제거하도록 설계된 스타일시트 접근 방식이다. `Reset CSS`를 적용하면 개발자는 빈 캔버스에서 시작하여 내장된 margin, padding, 폰트사이즈 및 기타 스타일을 제거하여 다양한 브라우저에서 일관성을 보장할 수 있다. 이 기술은 웹 프로젝트 전체에서 보다 예측 가능한 스타일 지정 프로세스를 촉진한다.
가장 잘 알려진 Reset CSS 중 하나는 Eric Meyer가 만든 것이다. Eric Meyer는 margin, padding 및 폰트사이즈를 0 또는 기타 일관된 값으로 설정하여 모든 요소의 모양을 표준화한다. `Reset CSS`는 완전한 솔루션이 아닌 시작점을 제공하므로 웹 개발자가 특정 디자인 요구 사항에 맞게 이 기반을 사용자 정의하고 구축하는 것이 중요하다.

## box-sizing 속성

box-sizing CSS 속성은 브라우저가 요소의 너비와 높이를 계산하는 방법을 결정한다. 이 속성은 레이아웃 설계에서 중요한 역할을 하며, 주로 두 가지 값(content-box와 border-box)을 사용한다.

### content-box (기본값)

content-box는 CSS의 기본 박스 모델이다. 이 설정을 사용할 때, 요소의 width와 height 속성은 내용(content) 영역의 크기를 지정하며, padding, border, margin은 이 크기에 추가된다. 결과적으로, 요소의 전체 크기는 지정된 width와 height에 padding, border의 두께가 더해진 값이 된다.

```css
.box {
  box-sizing: content-box;
  width: 300px; /*내용의 너비 */
  padding: 10px; /* 내용과 border 사이의 공간 */
  border: 5px solid black; /* border 두께 */
  /* 실제 박스의 너비 = 300px + 20px(양쪽 padding) + 10px(양쪽 border) = 330px*/
}
```

### border-box

border-box를 사용할 때, 요소의 width와 height는 padding과 border를 포함한 요소의 전체 크기를 지정한다. margin은 여전히 이 크기에 포함되지 않는다. 이 설정은 요소의 크기를 더 예측하기 쉽게 만들어, 레이아웃 설계를 단순화한다.

```css
.box {
  box-sizing: border-box;
  width: 300px; /*border와 padding을 포함한 너비 */
  padding: 10px; /* 내용과 border 사이의 공간 */
  border: 5px solid black; /* border의 두께 */
  /* 실제 박스의 너비 = 300px (padding과 border 포함)*/
}
```

## word-break 속성

CSS의 word-break 속성은 줄 끝에 도달했을 때 단어가 어떻게 끊어지는지 지정하는 데 사용된다. 이는 요소 내의 텍스트 오버플로를 처리하는 데 특히 유용하다. `break-all` 또는 `keep-all`과 같은 값을 설정함으로써 개발자는 임의의 지점에서 단어 분리를 허용할지 또는 함께 유지할지 여부를 제어할 수 있으며, 이는 특히 다양한 언어 및 조판 요구 사항을 처리하는 데 유용할 수 있다​.

## Theme, ThemeProvider

### Theme

`theme`은 애플리케이션에서 반복적으로 사용되는 스타일 값(예: 색상, 글꼴 크기, margin 등)을 저장하는 자바스크립트 객체이다. `theme`을 사용함으로써, 이러한 값들을 하드 코딩하는 대신, 중앙 집중식으로 관리하고 재사용할 수 있다. 이는 유지 관리를 용이하게 하며, `theme`을 변경하거나 여러 `theme` 사이를 전환할 때 유용하다.

### ThemeProvider

`ThemeProvider`는 React 컴포넌트 트리에 `theme`을 제공하는 컴포넌트이다. 이 컴포넌트는 styled-components 라이브러리에 포함되어 있으며, `theme` 객체를 props로 받아, 해당 `theme`을 자식 컴포넌트에게 전달한다. 자식 컴포넌트는 이 `theme` 객체를 사용하여 조건부 스타일링을 수행할 수 있다.

먼저, `theme` 객체를 정의

```js
const theme = {
  colors: {
    primary: "#007bff",
    secondary: "#6c757d",
  },
  fontSizes: {
    small: "12px",
    medium: "16px",
    large: "20px",
  },
};
```

그런 다음, `ThemeProvider`를 사용하여 애플리케이션에 `theme`을 적용

```jsx
import { ThemeProvider } from 'styled-components';
import theme from './theme'; // 위에서 정의한 `theme` 객체

function App() {
  return (
    <ThemeProvider theme={theme}>
      <YourComponent />
    </ThemeProvider>
  );
}
```

```jsx
import styled from 'styled-components';

const Button = styled.button`
  background-color: ${props => props.theme.colors.primary};
  color: white;
  font-size: ${props => props.theme.fontSizes.medium};
`;

function YourComponent() {
  return <Button>Click me</Button>;
}
```

`ThemeProvider`와 `theme`을 사용하는 접근 방식은 애플리케이션의 스타일링을 유연하고 일관되게 관리할 수 있게 해준다. 이 방식은 `theme` 변경이나 다양한 `theme` 사이의 전환을 쉽게 하며, 스타일 관련 값들을 중앙 집중식으로 관리할 수 있게 해준다.
