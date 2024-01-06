---
title: Github 블로그 사이드 메뉴 배경 이미지 변경
date: 2024-01-06 21:26:00 +0900
categories: [Github Blog]
tags: [Github Blog]     # TAG names should always be lowercase
---

## Github 사이드바 메뉴 배경 이미지 변경

안녕하세요. Winey 입니다.<br>
이번 포스트에서 블로그 사이드 메뉴의 배경 이미지를 변경하는 방법에 대해서 공유 하겠습니다.<br>
<br>
원하는 동작은 Chripy에서 제공되는 `dark|light` 테마에 따라 사이드 메뉴의 이미지가 변경 되게 하려고 합니다.<br>
<br>

<a href='/assets/post/2024-01-06/sidebar.zip' download> 사이드 메뉴 이미지 다운로드 </a>

---

## 테마 변경 시 HTML/CSS에 적용되는 내용 확인 

먼저 현재 Chripy에서 `dark|light` 테마에 따라 HTML과 CSS가 어떻게 변경되는지 파악하는 방법을 설명 하겠습니다.<br>
먼저 본인의 로컬 PC에서 `ruby prompt`를 이용하여 블로그를 실행 합니다.<br>
```bash
winey-dev.github.io> jekyll serve
...생략...
    http://localhost:4000
```

해당 [URL](http://localhost:4000)에 접속 후 `F12` 눌러 봅시다.<br>
그런 상태에서 Theme 아이콘을 클릭하여 변경되는 내용을 우측 화면에서 확인 해보면 됩니다.<br>
<br> 

![Desktop View](/assets/post/2024-01-06/mode_toggle.gif)

> 이 블로그 포스팅 당시 이미 배경 이미지를 변경하여 해당 영상은 Chripy demo 싸이트를 이용했습니다.
<br>

![Desktop View](/assets/post/2024-01-06/light_html_css.png)
![Desktop View](/assets/post/2024-01-06/dark_html_css.png)

dark mode 전환 시 html에서 달라지는 요소는 `data-mode`가 추가되는 것이고

```html
<html lang="en" data-mode="dark">
```

css에서는 `var(--sidebar-bg);` 에 설정 색상이 달라지는 것을 확인했습니다.
```css
background: [색상] var(--sidebar-bg);
```
<br>
<br>

---

## 변경하는 부분 

테마 변경 시 `--sidebar-bg` 변수의 색상만 변경되는 것을 위에서 확인했습니다..<br>
해당 변수는 `/_sass/colors/` 폴더 안에 각각 `typography-dark.scss`와 `typography-light.scss` 파일에 선언되어 있음으로 해당 파일에서 수정이 필요합니다.<br>
이제 해당 파일에 각각 image 설정을 위한 변수를 추가하고 해당 설정을 CSS에 추가 하면 됩니다.

### 배경 이미지 변수 추가
```scss
/* 파일 위치 /_sass/colors/typography-dark.scss */
  /* Sidebar */
  /*... 생략 ...*/
  --sidebar-bg-image: url('/assets/img/sidebar/dark_sidebar.png');

/* 파일 위치 /_sass/colors/typography-light.scss */
  /* Sidebar */
  /*... 생략 ...*/
  --sidebar-bg-image: url('/assets/img/sidebar/light_sidebar.png');

```

### CSS 적용
```css
/* 파일 위치 /_sass/addon/commons.scss */

#sidebar {
  @include pl-pr(0);

  /*... 생략 ...*/
  background-image: var(--sidebar-bg-image);
  background-size: cover;  /*이미지의 size가 보여질 부분의 사이즈와 다른 경우에는 이미지 크기를 꽉차게 만든다 */
  background-repeat: no-repeat; /*이미지의 size가 보여질 부분의 사이즈와 다른 경우 이미지가 반복하여 나오는데, 반복하지 않겠다*/
  /* background: var(--sidebar-bg); 기존 내용 주석 */
```

### Light Mode

![Desktop View](/assets/post/2024-01-06/light_view.jpg)

### Dark Mode
![Desktop View](/assets/post/2024-01-06/dark_view.jpg)


## 마무리 

 사이드 메뉴 커스터마이징을 진행하면서 사용한 이미지는 디자인쪽에서 일하는 누나에게 부탁하려고 했지만 바쁘신 관계로 .... 직접 PPT로 제작해 보았습니다.. 해당 이미지는 저작권이 없음으로 만약 맘에 들으셨다면 ... 마음대로 다운로드 하여 사용하셔도 됩니다. 수정도 가능하게 원본 PPT도 첨부합니다.<br>

<a href='/assets/post/2024-01-06/sidebar.zip' download> 사이드 메뉴 이미지 다운로드 </a>
 
<br>
 블로그를 쓰면서 다른 사람이 쓴 블로그 글과 중복되는 내용을 줄이고 개인적인 경험을 위주로 작성하다보니 생략되는 내용이들이 존재합니다. 생략된 내용들을 작성하는 것이 옳은지에 대한 고민이 많은데 조금 더 고민해보고 필요하다면 내용을 추가하겠습니다. <br>

<br>
 


---