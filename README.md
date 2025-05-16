# 반응형 이미지와 미디어, Flexbox 정리

## 반응형 이미지

### CSS 설정 예시
```css
img {
  width: 100%;
  max-width: 100%;
  height: auto; /* 생략 가능 */
}
```

- 이미지 너비를 고정값이 아닌 `%`로 지정하면 반응형 웹에 적합
- `max-width`를 100%로 설정해 부모 요소 너비를 초과하지 않도록 제한

### `<picture>` 요소
다양한 화면 크기에 따라 다른 이미지를 제공할 수 있도록 하는 HTML5 태그

```html
<picture>
  <source srcset="../images/lime-1000.jpg" media="(min-width:1024px)">
  <source srcset="../images/lime-740.jpg" media="(min-width:768px)">
  <source srcset="../images/lime-300.jpg" media="(min-width:320px)">
  <img src="../images/lime.jpg" alt="lime" style="max-width:100%">
</picture>
```

- `<img>`는 반드시 포함되어야 하며, 기본 이미지 혹은 오류 시 대체 이미지로 사용됨

---

## 반응형 비디오

### 일반적인 반응형 비디오 설정
```css
video {
  width: 100%;
  max-width: 100%;
}
```

### YouTube 등 외부 비디오 임베드 시
```html
<body>
  <div class="videoContainer">
    <iframe src="..."></iframe>
  </div>
</body>

<style>
body { text-align: center; }

.videoContainer {
  position: relative;
  padding-bottom: 56.25%; /* 16:9 비율 */
  height: 0;
}

.videoContainer iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
```

- `height`가 아닌 `padding-bottom`을 사용하는 이유:
  - `height`는 부모 요소의 높이를 기준으로 비율이 적용됨
  - `padding-bottom`은 부모의 너비를 기준으로 높이를 정함 → 반응형 구현에 유리

---

## Flexbox 정리

### display 설정
```css
display: flex;        /* 블록 요소 */
display: inline-flex; /* 인라인 요소 */
```

부모 요소에 설정하여 자식 요소들을 정렬함

### flex-direction
주축 방향 설정
- `row` (기본값), `row-reverse`
- `column`, `column-reverse`

### flex-wrap
한 줄에 요소가 다 들어가지 않을 경우 줄 바꿈 여부 설정
- `nowrap` (기본값)
- `wrap`, `wrap-reverse`

### flex-flow
`flex-direction`과 `flex-wrap`을 한 줄로 지정
```css
flex-flow: row nowrap;
```

### justify-content
주축 방향 정렬
- `flex-start`, `flex-end`, `center`
- `space-between`, `space-around`

### align-items
교차축 방향 정렬
- `flex-start`, `flex-end`, `center`
- `baseline`, `stretch`

### align-self
개별 항목에 적용되는 교차축 정렬
- `flex-start`, `flex-end`, `center`, `baseline`, `stretch`

### align-content
교차축 정렬 (두 줄 이상일 때만 적용)
- `flex-start`, `flex-end`, `center`
- `space-between`, `space-around`, `stretch`

---

## Flex 속성 (자식 요소에 적용)

```css
flex: 1 1 auto;
```
- `flex-grow`: 너비 증가 비율 (기본값 0)
- `flex-shrink`: 너비 감소 비율 (기본값 1)
- `flex-basis`: 기본 너비 (기본값 auto)

### 주요 개념
- 단위가 주어진 `flex-basis` 값은 고정됨
- `auto`는 기존 `width`, `height` 속성 사용
- `flex`는 `grow shrink basis` 순으로 한 줄에 작성 가능
- `flex-grow` 제외하고 생략 가능
- `flex-basis`를 생략하면 기본값은 `0`

---

## 기타 속성 정리

### 반응형 박스 설정
```css
*, *::before, *::after {
  box-sizing: border-box;
}
```

- 전체 요소에 가변 크기 설정 시 사용

### 이미지/비디오 맞춤 조정

```css
object-fit: cover;
```

- HTML 콘텐츠(`<img>`, `<video>`)가 컨테이너에 꽉 차게 표시되도록 함

### 배경 이미지 조정

```css
background-size: cover;
```

- 배경 이미지가 요소의 크기에 맞게 꽉 차도록 조정

---

## 텍스트 및 요소 정렬

### text-align
- 블록 요소 안에서 인라인 요소, 인라인-블록 요소 정렬
- 예: `text-align: center;`

---

## CSS 선택자

### `:nth-child`
```css
:nth-child(odd)  /* 홀수 번째 요소 */
:nth-child(even) /* 짝수 번째 요소 */
```

---

## 용어 요약

- **가세**: 가로/세로
- **로컬**: Row/Column
- **호버**: Horizontal/Vertical
- **오열**: 오/열 (오른쪽/열)

---
