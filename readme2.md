# CSS 기초 노트

CSS를 처음 배울 때 필요한 개념과 자주 쓰는 속성을 순서대로 정리한 문서입니다. 예제는 설명을 위한 것이며, 직접 작성해 보면서 결과를 확인해 보세요.

## 목차

- [1. CSS란 무엇인가](#1-css란-무엇인가)
- [2. CSS 작성 방법](#2-css-작성-방법)
- [3. 선택자](#3-선택자)
- [4. 스타일이 적용되는 순서](#4-스타일이-적용되는-순서)
- [5. 글자와 텍스트](#5-글자와-텍스트)
- [6. 목록 스타일](#6-목록-스타일)
- [7. 박스 모델](#7-박스-모델)
- [8. 요소 배치와 display](#8-요소-배치와-display)
- [9. Flex 레이아웃](#9-flex-레이아웃)
- [10. position으로 위치 지정](#10-position으로-위치-지정)
- [11. 이어서 공부할 주제](#11-이어서-공부할-주제)

## 1. CSS란 무엇인가

HTML이 웹 페이지의 내용과 구조를 만든다면, CSS는 그 구조의 모양과 배치를 정합니다. 예를 들어 글자색, 크기, 여백, 배경색, 요소의 위치를 CSS로 지정합니다.

CSS는 **Cascading Style Sheets**의 약자입니다. Cascading은 여러 스타일 규칙이 함께 적용될 때 정해진 우선순위에 따라 결과가 결정되는 특성을 가리킵니다.

## 2. CSS 작성 방법

CSS 규칙은 보통 다음 형태로 씁니다.

```css
선택자 {
  속성: 값;
}
```

- **선택자**: 어떤 HTML 요소를 꾸밀지 고릅니다.
- **속성**: 바꾸려는 항목입니다. 예: `color`, `font-size`
- **값**: 속성에 지정할 내용입니다. 예: `red`, `24px`

### 인라인 스타일

HTML 요소의 `style` 속성에 CSS를 직접 씁니다. 작은 실험에는 편하지만, 스타일과 HTML 내용이 섞여 관리가 어려워질 수 있습니다.

```html
<p style="color: red">빨간색 문장</p>
```

### 내부 스타일 시트

HTML 문서의 `<head>` 안에 `<style>` 요소를 만들고 CSS를 씁니다. 해당 HTML 문서 안에서 사용할 스타일에 적합합니다.

```html
<head>
  <style>
    p {
      color: blue;
      text-align: center;
    }
  </style>
</head>
```

### 외부 스타일 시트

CSS를 별도의 `.css` 파일에 저장한 뒤 HTML의 `<head>`에서 연결합니다. 여러 HTML 문서가 같은 CSS 파일을 함께 사용할 수 있어 일반적으로 많이 쓰는 방법입니다.

```html
<head>
  <link rel="stylesheet" href="css/style.css" />
</head>
```

`css/style.css` 파일:

```css
h1 {
  color: red;
}
```

## 3. 선택자

선택자는 스타일을 적용할 HTML 요소를 고르는 문법입니다.

### 전체 선택자 `*`

문서의 모든 요소를 선택합니다. 기본 여백을 초기화할 때 자주 사용합니다.

```css
* {
  margin: 0;
  padding: 0;
}
```

### 타입 선택자

HTML 태그 이름으로 같은 태그를 모두 선택합니다. 아래 규칙은 모든 `<h3>` 요소에 적용됩니다.

```css
h3 {
  color: purple;
  font-size: 36px;
}
```

### 클래스 선택자 `.이름`

HTML의 `class` 값으로 요소를 선택합니다. 클래스는 여러 요소에 반복해서 사용할 수 있고, 한 요소에 여러 클래스를 지정할 수도 있습니다.

```html
<div class="card highlight">내용</div>
```

```css
.card {
  padding: 16px;
}

.highlight {
  background-color: yellow;
}
```

클래스 이름 앞에는 CSS에서 점(`.`)을 붙입니다. HTML의 `class` 값에는 점을 붙이지 않습니다.

### 아이디 선택자 `#이름`

HTML의 `id` 값과 일치하는 요소를 선택합니다. `id`는 한 문서 안에서 고유하게 사용해야 합니다. 스타일을 적용할 때는 보통 재사용하기 쉬운 클래스를 더 많이 사용합니다.

```html
<div id="container">내용</div>
```

```css
#container {
  width: 500px;
  margin: 20px auto;
}
```

### 그룹 선택자 `,`

여러 선택자에 같은 규칙을 적용합니다. 쉼표로 선택자를 구분합니다.

```css
ul,
li {
  list-style: none;
}
```

### 선택자 간단 비교

| 선택자 | 고르는 대상 | 예시 |
| --- | --- | --- |
| `*` | 모든 요소 | `* { box-sizing: border-box; }` |
| `p` | 모든 `<p>` 요소 | `p { color: #333; }` |
| `.notice` | `class="notice"`인 요소 | `.notice { color: red; }` |
| `#main` | `id="main"`인 요소 | `#main { width: 800px; }` |

## 4. 스타일이 적용되는 순서

한 요소에 여러 규칙이 적용되면 브라우저는 **출처, 중요도, 선택자의 구체성, 작성 순서** 등을 고려해 최종 스타일을 정합니다.

초급 단계에서는 다음을 기억하면 좋습니다.

1. 같은 속성에 여러 규칙이 걸리면, 더 구체적인 선택자가 대체로 우선합니다.
2. 선택자의 구체성이 같으면 뒤에 작성된 규칙이 우선합니다.
3. `!important`는 우선순위 계산에 영향을 크게 주므로 꼭 필요한 경우가 아니면 사용하지 않습니다.

예를 들어 클래스 선택자는 타입 선택자보다 구체적이므로 다음 경우에는 `.message`의 색이 적용됩니다.

```css
p {
  color: blue;
}

.message {
  color: red;
}
```

```html
<p class="message">이 문장은 빨간색입니다.</p>
```

위의 순서는 모든 CSS 상황을 설명하는 완전한 우선순위표는 아닙니다. 사용자 설정, 브라우저 기본 스타일, `!important`, 레이어 등도 결과에 영향을 줄 수 있습니다.

### 상속

일부 속성은 부모 요소에 지정하면 자식 요소에도 전달됩니다. 글자색과 글꼴처럼 글자와 관련된 속성이 대표적입니다. 모든 속성이 상속되는 것은 아닙니다. 예를 들어 부모의 `margin`이나 `border`가 자식에게 자동으로 전달되지는 않습니다.

```css
body {
  color: #29292c;
  font-family: sans-serif;
}
```

## 5. 글자와 텍스트

### 글꼴: `font-family`

사용할 글꼴을 지정합니다. 앞쪽 글꼴을 사용할 수 없으면 뒤쪽 글꼴을 차례로 시도합니다. 글꼴 이름에 공백이 있으면 따옴표로 감쌉니다.

```css
body {
  font-family: Arial, "Malgun Gothic", sans-serif;
}
```

### 글자 크기: `font-size`

글자 크기는 `px`, `em`, `rem`, `%` 등으로 지정합니다.

- `px`: CSS에서 사용하는 길이 단위입니다. 화면의 실제 하드웨어 픽셀과 항상 일대일로 대응하지는 않습니다.
- `em`: 현재 요소의 글자 크기 등을 기준으로 계산됩니다. 부모의 글자 크기에 영향을 받는 경우가 많습니다.
- `rem`: 루트 요소(`<html>`)의 글자 크기를 기준으로 계산됩니다.
- `%`: 문맥에 따라 기준이 달라집니다. 글자 크기에서 사용하면 부모 요소의 글자 크기를 기준으로 합니다.

```css
html {
  font-size: 16px;
}

.small {
  font-size: 0.875rem;
}
```

### 글자 굵기: `font-weight`

글자를 얼마나 굵게 표시할지 정합니다. `normal`, `bold` 또는 `100`부터 `900`까지의 숫자를 사용할 수 있습니다. 실제 표시 가능한 굵기는 사용 중인 글꼴에 따라 다릅니다.

```css
.title {
  font-weight: 700;
}
```

### 웹 폰트: `@font-face`

웹 폰트 파일을 프로젝트에 두고 CSS에서 등록해 사용할 수 있습니다. 파일 경로는 CSS 파일을 기준으로 작성하는 경우가 일반적입니다.

```css
@font-face {
  font-family: "MyFont";
  src: url("../assets/my-font.woff2") format("woff2");
  font-weight: 400;
  font-style: normal;
}
```

### 글자색: `color`

색상은 16진수, `rgb()`, `rgba()`, `hsl()` 등으로 지정할 수 있습니다.

```css
.title {
  color: #f60;
}

.overlay-text {
  color: rgba(0, 0, 0, 0.7);
}
```

`rgba()`와 `hsla()`의 마지막 값은 투명도입니다. `0`은 완전히 투명하고 `1`은 완전히 불투명합니다.

### 텍스트 정렬: `text-align`

요소 안에 있는 인라인 내용이나 텍스트를 가로 방향으로 정렬합니다. 블록 요소 자체를 가운데 놓는 속성은 아닙니다. 블록 요소를 가운데 배치할 때는 너비와 `margin` 등을 사용합니다.

```css
p {
  text-align: center;
}
```

- `left`, `right`: 왼쪽 또는 오른쪽 정렬
- `center`: 가운데 정렬
- `justify`: 양쪽 정렬
- `start`, `end`: 글의 쓰기 방향을 기준으로 시작 또는 끝에 정렬

### 줄 간격: `line-height`

텍스트 줄의 높이를 정합니다. 단위 없는 숫자를 쓰면 글자 크기의 배수로 계산되어 편리합니다.

```css
p {
  font-size: 16px;
  line-height: 1.6;
}
```

위 예시에서 줄 높이는 글자 크기의 1.6배입니다. `px` 같은 길이 단위도 사용할 수 있습니다.

### 밑줄·취소선: `text-decoration`

```css
a {
  text-decoration: none;
}

.deleted {
  text-decoration: line-through;
}
```

주요 값은 `underline`(밑줄), `line-through`(취소선), `overline`(윗줄), `none`(장식 없음)입니다.

### 글자 그림자: `text-shadow`

가로 오프셋, 세로 오프셋, 흐림 반경, 색상 순으로 지정합니다.

```css
.title {
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}
```

### 영문 대소문자: `text-transform`

화면에 표시되는 영문자의 대소문자 형태를 바꿉니다. 원래 HTML 텍스트 자체를 수정하지는 않습니다.

- `none`: 변환하지 않음
- `capitalize`: 각 단어의 첫 글자를 대문자로 표시
- `uppercase`: 모두 대문자로 표시
- `lowercase`: 모두 소문자로 표시

### 글자 간격: `letter-spacing`, `word-spacing`

```css
p {
  letter-spacing: 0.02em;
  word-spacing: 0.1em;
}
```

`letter-spacing`은 글자 사이 간격, `word-spacing`은 단어 사이 간격을 조절합니다.

## 6. 목록 스타일

### 마커 모양: `list-style-type`

목록의 불릿이나 번호 모양을 정합니다.

```css
ul {
  list-style-type: square;
}

ol {
  list-style-type: decimal-leading-zero;
}
```

자주 쓰는 값은 `disc`, `circle`, `square`, `decimal`, `decimal-leading-zero`, `lower-roman`, `upper-roman`, `lower-alpha`, `upper-alpha`, `none`입니다.

### 이미지 마커: `list-style-image`

```css
ul {
  list-style-image: url("../assets/bullet.svg");
}
```

이미지가 로드되지 않을 때를 대비해 마커 모양도 함께 지정하는 방법이 있습니다.

### 마커 위치: `list-style-position`

- `inside`: 마커를 목록 항목의 내용 영역 안쪽에 둡니다.
- `outside`: 마커를 내용 영역 바깥쪽에 둡니다. 기본값입니다.

```css
ul {
  list-style-position: inside;
}
```

### 한 번에 지정: `list-style`

종류, 이미지, 위치를 한꺼번에 지정하는 축약 속성입니다.

```css
ul {
  list-style: square inside;
}
```

## 7. 박스 모델

브라우저는 대부분의 HTML 요소를 상자처럼 배치합니다. 상자는 안쪽에서 바깥쪽 순서로 **콘텐츠 → padding(안쪽 여백) → border(테두리) → margin(바깥 여백)**으로 구성됩니다.

```text
margin
┌──────────────────────────┐
│ border                   │
│  ┌────────────────────┐  │
│  │ padding            │  │
│  │  ┌──────────────┐  │  │
│  │  │ 콘텐츠        │  │  │
│  │  └──────────────┘  │  │
│  └────────────────────┘  │
└──────────────────────────┘
```

### 너비와 높이: `width`, `height`

`width`는 너비, `height`는 높이를 지정합니다. `px`, `%`, `rem` 등의 단위를 사용할 수 있습니다. `%`는 보통 부모 요소의 크기를 기준으로 계산됩니다. `auto`는 속성에 따라 브라우저가 크기를 계산하도록 합니다.

### 크기 계산: `box-sizing`

기본값인 `content-box`에서는 `width`와 `height`가 콘텐츠 영역의 크기입니다. padding과 border는 그 바깥에 더해집니다.

`border-box`에서는 지정한 너비와 높이에 콘텐츠, padding, border가 포함됩니다. 레이아웃의 전체 크기를 예상하기 쉬워 자주 사용합니다.

```css
* {
  box-sizing: border-box;
}
```

### 네 방향 축약 표기

`margin`, `padding`, `border-width` 등은 값을 1~4개 써서 각 방향을 지정할 수 있습니다.

```css
.box {
  margin: 10px;           /* 네 방향 모두 10px */
  padding: 10px 20px;     /* 위아래 10px, 좌우 20px */
  border-width: 1px 2px 3px; /* 위 1px, 좌우 2px, 아래 3px */
  margin: 1px 2px 3px 4px; /* 위, 오른쪽, 아래, 왼쪽 순서 */
}
```

네 값은 **위 → 오른쪽 → 아래 → 왼쪽** 순서입니다.

### 테두리: `border`

`border` 축약 속성은 두께, 선 모양, 색상을 함께 지정합니다.

```css
.box {
  border: 2px solid #333;
}
```

선 모양에는 `solid`(실선), `dotted`(점선), `dashed`(짧은 선), `double`(이중선) 등이 있습니다.

### 모서리 둥글게: `border-radius`

```css
.box {
  border-radius: 12px;
}

.circle {
  width: 100px;
  height: 100px;
  border-radius: 50%;
}
```

`50%`는 요소 크기에 대한 비율입니다. 너비와 높이가 같은 상자라면 원이 되고, 크기가 다르면 타원처럼 보입니다. 네 값을 지정하면 왼쪽 위부터 시계 방향으로 왼쪽 위, 오른쪽 위, 오른쪽 아래, 왼쪽 아래 모서리에 적용됩니다.

### 그림자: `box-shadow`

가로 오프셋, 세로 오프셋, 흐림 반경, 퍼짐 반경(선택), 색상 순으로 지정할 수 있습니다. `inset`을 넣으면 안쪽 그림자가 됩니다.

```css
.card {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}
```

### `margin`과 `padding`

- `margin`: 요소 바깥의 여백입니다.
- `padding`: 테두리와 콘텐츠 사이의 안쪽 여백입니다.

```css
.box {
  width: 300px;
  margin: 50px auto; /* 위아래 50px, 좌우는 남는 공간을 나눠 가운데 배치 */
  padding: 16px;
  border: 4px solid #000;
}
```

좌우 `margin`이 `auto`이면, 정해진 너비가 있고 남는 공간이 있을 때 블록 요소를 가운데 배치하는 데 사용할 수 있습니다.

세로로 맞닿은 블록 요소의 위아래 margin은 단순히 더해지지 않고 하나처럼 보이는 경우가 있습니다. 이를 **margin 중첩**이라고 합니다. 모든 상황에서 발생하는 것은 아니며, 부모·자식 관계나 레이아웃 방식 등에 따라 달라집니다.

## 8. 요소 배치와 display

`display`는 요소가 레이아웃에서 어떤 방식으로 상자를 만들지 정합니다.

- `block`: 새 줄에서 시작하고, 기본적으로 가능한 너비를 차지합니다. `width`와 `height`를 지정할 수 있습니다.
- `inline`: 문장 안에 놓이며 필요한 만큼 공간을 차지합니다. 일반적으로 `width`와 `height`가 기대한 방식으로 적용되지 않습니다.
- `inline-block`: 문장 안에서 옆으로 배치되면서 너비와 높이를 지정할 수 있습니다.
- `none`: 보이지 않고 레이아웃 공간도 차지하지 않습니다.
- `flex`: 자식 요소를 유연하게 배치하는 Flex 컨테이너가 됩니다.

`div`, `p`는 기본적으로 block이고, `span`, `a`, `strong`은 기본적으로 inline입니다. 요소의 기본 display는 CSS로 바꿀 수 있습니다.

`inline-block`으로 메뉴를 나란히 배치하는 간단한 예입니다.

```css
.menu-item {
  display: inline-block;
  padding: 8px;
  border: 1px solid #333;
}
```

### `float`과 `clear`

`float`은 요소를 왼쪽이나 오른쪽으로 띄우고, 주변의 텍스트가 그 옆을 흐르도록 하던 레이아웃 방식입니다. 요즘 일반적인 페이지 레이아웃은 Flex나 Grid를 더 많이 사용하지만, 기존 코드에서 `float`을 만날 수 있습니다.

`clear`는 요소가 앞선 float 요소 옆에 흐르지 않도록 합니다.

```css
.next-section {
  clear: both;
}
```

## 9. Flex 레이아웃

Flex는 한 방향으로 요소를 배치하고 정렬할 때 편리합니다. Flex를 적용한 부모를 **flex container**, 그 직계 자식을 **flex item**이라고 합니다.

```css
.container {
  display: flex;
}
```

기본값에서는 자식이 가로 방향으로 배치됩니다.

### 주축과 교차축

- **주축(main axis)**: `flex-direction`으로 정하는 기본 배치 방향입니다.
- **교차축(cross axis)**: 주축에 수직인 방향입니다.

기본값 `row`에서는 주축이 가로이고 교차축이 세로입니다. `column`으로 바꾸면 주축이 세로, 교차축이 가로가 됩니다.

### 방향과 줄바꿈

```css
.container {
  display: flex;
  flex-direction: row; /* row, row-reverse, column, column-reverse */
  flex-wrap: wrap;     /* nowrap, wrap, wrap-reverse */
}
```

`nowrap`이 기본값입니다. `wrap`을 쓰면 한 줄에 들어가지 않는 항목이 다음 줄로 넘어갈 수 있습니다.

### 주축 정렬: `justify-content`

```css
.container {
  display: flex;
  justify-content: space-between;
}
```

- `flex-start`: 주축 시작점에 모읍니다.
- `flex-end`: 주축 끝점에 모읍니다.
- `center`: 가운데에 모읍니다.
- `space-between`: 첫 항목과 마지막 항목을 양 끝에 두고 사이 공간을 나눕니다.
- `space-around`: 항목 주변에 공간을 둡니다. 양 끝 공간은 항목 사이 공간보다 작게 보입니다.
- `space-evenly`: 항목 사이와 양 끝의 간격을 균등하게 둡니다.

### 교차축 정렬: `align-items`

한 줄 안에서 각 항목을 교차축 방향으로 정렬합니다.

- `stretch`: 교차축 크기가 자동인 항목을 남는 공간에 맞춰 늘립니다.
- `flex-start`, `flex-end`: 교차축의 시작 또는 끝에 둡니다.
- `center`: 교차축 가운데에 둡니다.
- `baseline`: 텍스트의 기준선을 맞춥니다.

### 여러 줄 정렬: `align-content`

항목이 여러 줄이고 교차축 방향에 여유 공간이 있을 때 줄 전체를 정렬합니다. 한 줄만 있을 때는 효과가 없습니다. `flex-wrap: wrap`과 함께 이해하면 좋습니다. 주요 값은 `flex-start`, `flex-end`, `center`, `space-between`, `space-around`, `space-evenly`, `stretch`입니다.

### 개별 항목 정렬: `align-self`

특정 flex item 하나의 교차축 정렬을 따로 지정합니다.

```css
.item-special {
  align-self: center;
}
```

## 10. `position`으로 위치 지정

`position`은 요소를 일반적인 문서 흐름에서 어떻게 배치할지 정합니다. `top`, `right`, `bottom`, `left`는 위치가 지정된 요소의 오프셋을 정할 때 사용합니다.

- `static`: 기본값. 일반 문서 흐름에 따라 배치됩니다. `top` 등의 오프셋은 적용되지 않습니다.
- `relative`: 원래 위치를 기준으로 이동합니다. 원래 자리는 유지됩니다.
- `absolute`: 일반 문서 흐름에서 빠져나와 배치됩니다. 보통 가장 가까운 위치 지정 조상을 기준으로 합니다.
- `fixed`: 보통 브라우저 화면을 기준으로 고정되어 스크롤해도 같은 위치에 보입니다. 조상의 특정 속성이 기준을 바꿀 수 있습니다.
- `sticky`: 평소에는 흐름에 따라 움직이다가 스크롤 위치가 임계점에 닿으면 붙어 있는 것처럼 동작합니다. 보통 `top` 등 임계 위치를 지정해야 합니다.

### `absolute`의 기준

`absolute` 요소는 보통 가장 가까운 `position` 값이 `static`이 아닌 조상을 기준으로 배치됩니다. 그런 조상이 없다면 초기 기준 블록을 사용합니다. 그래서 특정 부모를 기준으로 배치하고 싶을 때 그 부모에 `position: relative`를 지정하는 방법을 자주 씁니다.

```css
.header {
  position: relative;
}

.submenu {
  position: absolute;
  top: 100%; /* 기준이 되는 상자 높이만큼 아래 */
  left: 0;
}
```

`top: 100%`의 기준과 위치는 실제로 어떤 조상이 기준이 되었는지에 따라 달라집니다. 부모를 기준으로 만들려면 그 부모의 `position`을 확인하세요.

### 겹치는 순서: `z-index`

요소가 겹칠 때 앞뒤 순서를 조정합니다. 숫자가 큰 요소가 위에 보이는 경우가 많지만, 서로 다른 쌓임 맥락에 속하면 단순히 숫자만 비교할 수 없습니다. `position`이 지정된 요소에서 주로 사용하며, Flex item 등 일부 상황에도 적용됩니다.

## 11. 이어서 공부할 주제

기존 노트의 다음 주제는 제목만 정리되어 있어, 이 문서에서는 학습 예정 목록으로 남겨 둡니다.

- 이미지, 그라데이션, 배경
- 고급 선택자
- 트랜지션과 애니메이션
- 반응형 웹과 미디어 쿼리
