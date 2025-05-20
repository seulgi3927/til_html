# JS 적용

- JS 는 2가지로 크게 분류됩니다.
- Node와 Web(웹브라우저)으로 분류합니다.

## JS 코딩 좋은 위치

- 가장 좋은 자리는 html 이 완료되는 시점.

```js
// html 의  document 가 모두 로드 되면 실행하기
// html 의  이미지, 파일 등등 리소스가 준비되면 실행
// 표준입니다.
window.addEventListener("load", function () {});

// html 만 로드 완료를 체크합니다.
window.addEventListener("DOMContentLoaded", function () {});
```

## 요소(Element) 선택법

```js
// DOM 만 완성화면 됩니다. 기준으로 코드를 진행함.
window.addEventListener("DOMContentLoaded", function () {
  // 우리가 원하는 요소(Element) 를 선택하는 법?
  // - Tag 를 선택하고 싶어요. (Tag Element)
  this.document.getElementsByTagName("header");
  this.document.getElementsByClassName("header");
  // - CSS 선택자를 이용해서 선택하고 싶어요. (Css Selector)
  this.document.querySelector(".header");
  this.document.querySelectorAll(".header");
  // - ID 선택자를 이용해서 선택하고 싶어요. (ID)
  this.document.getElementById("header");
});
```

- 예제

```js
// DOM 만 완성화면 됩니다. 기준으로 코드를 진행함.
window.addEventListener("DOMContentLoaded", function () {
  const header = this.document.querySelector(".header");
  console.log(header);
  const logo = this.document.querySelector(".logo");
  console.log(logo);
  const search = this.document.querySelector(".search");
  console.log(search);
  const member = this.document.querySelector(".header_top_right");
  console.log(member);
  const eventMenu = this.document.querySelector(".header_bottom_eventmenu");
  console.log(eventMenu);
}); // div 를 추천합니다.
```

## 다양한 이벤트의 이해

- 웹브라우저가 체크하는 변화를 `이벤트` 라고 함.
- 이벤트 작성법 3가지

### 1. 태그에 직접 이벤트 작성하기

```js
<태그 on이벤트="코드"></태그>
<header class="header" onclick="alert('안녕')"></header>
```

### 2. 요소에 속성으로 이벤트 작성하기

```js
요소.on이벤트 = function () {};
const header = this.document.querySelector(".header");
header.onclick = function () {
  alert("반가워");
};
```

### 3. 요소에 이벤트 핸들러로 이벤트 작성하기(표준)

```js
요소.addEventListener("이벤트", function () {});

const header = this.document.querySelector(".header");
header.addEventListener("click", function () {
  alert("표준 반가워");
});
```

### 4. 활용빈도가 높은 `윈도우 이벤트`

- `load` :
- `DOMContentLoaded` :
- `resize`: 웹브라우저 너비, 높이 변경시 발생
- `scroll` : 웹브라우저에 스크롤이 일어나면 발생

### 5. 활용빈도가 높은 `마우스 이벤트`

- `click` : 마우스 클릭(왼쪽)
- `mouseenter` : 마우스 커서가 요소에 걸쳐지면
- `mouseleave` : 마우스 커사가 요소에서 벗어나면

### 6. 활용빈도가 높은 `키보드 이벤트`

- `keyup` : 키보드에서 키 입력후 이벤트
- `keydown` : 키보드에서 키 입력시 이벤트
- `keypress` : 키보드에서 키 누르고 있으면 이벤트

### 7. 활용빈도가 높은 Form 관련 이벤트 (추후 정리)

## CSS 제어법

### 1. Inline 형태로 적용하기 (가끔 활용함)

- `대상.style.css속성 = "값"`

```js
// DOM 만 완성화면 됩니다. 기준으로 코드를 진행함.
// DOM 은 html 태그 구조를 말한다.
// ↓ 아래 문장은 html 이 완성되어졌다면 실행하자.
window.addEventListener("DOMContentLoaded", function () {
  // ↓ 아래 구문은 header 변수를 만들고 html (document) 에서 css 선택자로 값을 셋팅
    const header = this.document.querySelector(".header");
    const logo = this.document.querySelector(".logo");
    const search = this.document.querySelector(".search");
    const member = this.document.querySelector(".header_top_right");
    const eventMenu = this.document.querySelector(".header_bottom_eventmenu");
  
    // ↓ 윈도우에 스크롤이(scroll 이벤트) 일어나면 기능을 작동하겠다.
    this.window.addEventListener("scroll", function () {
      // ↓ 스크롤이 되었을 때 스크롤바의 Y 축의 상단 픽셀위치 값
      const scrollY = window.scrollY;

      // ↓ headerTop 영역의 높이값을 px 로 알고 싶다↓
      const headerTopH = this.document.querySelector(".header_top");
      console.log(headerTopH.offsetHeight); // 50px 출력
  
      // ↓ 만약 50 보다 작으면 전체 를 보이고, 그렇지 않으면 일부분을 숨긴다.
      if (scrollY <= headerTopH.offsetHeight) {
        // console.log("모두 보여라");
        logo.style.display = "block";
        eventMenu.style.display = "block";
      } else {
        // console.log("일부만 보여라");
        // ↓ 로고를 css 로 제어하겠다.
        logo.style.display = "none";
        eventMenu.style.display = "none";
        search.style.position = "absolute";
        search.style.left = "350px";
        search.style.top = "48px";
      }
    });
  });
  ```

  ### 2. CSS 클래스 활용하기 (적극 활용함)

  - `대상.classList.add("클래스명")`
- `대상.classList.remove("클래스명")`
- `대상.classList.toggle("클래스명")`
- `대상.classList.contain("클래스명")`

```js
// DOM 만 완성화면 됩니다. 기준으로 코드를 진행함.
// DOM 은 html 태그 구조를 말한다.(Document Object Model) : 객체
// 아래 문장은 html 이 완성되어졌다면 실행하자.
window.addEventListener("DOMContentLoaded", function () {
  // 아래 구문은 heder 변수를 만들고 html (document) 에서 css 선택자로 값을 셋팅
  const header = this.document.querySelector(".header");
  const headerTop = this.document.querySelector(".header_top");
  const logo = this.document.querySelector(".logo");
  const search = this.document.querySelector(".search");
  const member = this.document.querySelector(".header_top_right");
  const eventMenu = this.document.querySelector(".header_bottom_eventmenu");

  // 윈도우에 스크롤(scroll 이벤트)이 일어나면 기능을 작동하겠다.
  this.window.addEventListener("scroll", function () {
    // 스크롤이 되었을 때 스크롤바의 Y 축의 상단 픽셀위치값
    const scrollY = window.scrollY;

    // headerTop 영역의 높이값을 px 로 알고 싶다.
    const headerTopH = this.document.querySelector(".header_top");
    console.log(headerTopH.offsetHeight); //  50px 출력

    // 만약 50 보다 작으면 전체 를 보이고, 그렇지 않으면 일부분을 숨긴다.
    if (scrollY <= headerTopH.offsetHeight) {
      // console.log("모두 보여라");
      logo.style.display = "block";
      eventMenu.style.display = "block";
      // class 제거로 변경
      header.classList.remove("header_down");
      headerTop.classList.remove("header_top_down");
      search.classList.remove("search_down");
      member.classList.remove("member_down");
    } else {
      // console.log("일부만 보여라");
      // 로고를 css 로 제어하겠다.
      logo.style.display = "none";
      eventMenu.style.display = "none";
      // class 추가로 변경
      header.classList.add("header_down");
      headerTop.classList.add("header_top_down");
      search.classList.add("search_down");
      member.classList.add("member_down");
    }
  });
});
```

## 슬라이드 외부 라이브러리 활용하기

- 절대로 직접 만들지 마세요.
- `Swiper` : 가장 추천 (https://swiperjs.com/)
- `Slick` : 추천 (https://kenwheeler.github.io/slick/)
- `bwSlide` : 비추천 (https://bxslider.com/)

