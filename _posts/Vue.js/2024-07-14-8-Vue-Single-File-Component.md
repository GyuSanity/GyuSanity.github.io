---
layout: post
title: 8. Vue 싱글 파일 컴포넌트
category: Vue.js
tag: [Vue.js]
---

## Navigation Var
***[vue single file component](#vue-single-file-component)***
***[웹팩이란](#웹팩이란---detail--link)***
***[](#)***
***[](#)***

## [Vue Single File Component](https://joshua1988.github.io/vue-camp/vue/sfc.html)
- 싱글 파일 컴포넌트는 화면의 특정 영역에 대한 HTML, CSS, JS 코드를 한 파일에서 관리하는 방법

<details>

```javascript
<!-- .vue 파일 구조 -->
<template>
  <!-- html (뷰 컴포넌트의 표현단, 템플릿 문법) -->
</template>

<script>
  // 자바스크립트 (뷰 컴포넌트 내용)
</script>

<style>
  /* CSS (뷰 템플릿의 스타일링) */
</style>
```

</details>


- 싱글파일 컴포넌트인 vue 확장자의 경우 별도의 변환 과정이 필요하며, 뷰 로더가 수행(웹팩 로더 종류중 하나이며, vuecli로 프로젝트를 설정시 기본적으로 설정이 되어 있음)

## 웹팩이란? - Detail : [link](https://joshua1988.github.io/webpack-guide/webpack/what-is-webpack.html)
-  최신 프런트엔드 프레임워크에서 가장 많이 사용되는 모듈 번들러(Module Bundler)
- 모듈 번들러란 웹 애플리케이션을 구성하는 자원(HTML, CSS, Javscript, Images 등)을 모두 각각의 모듈로 보고 이를 조합해서 병합된 하나의 결과물을 만드는 도구

- `모듈` : 모듈이란 프로그래밍 관점에서 특정 기능을 갖는 작은 코드 단위를 의미하며, 웹팩에서의 모듈은  HTML, CSS, Javascript, Images, Font 등 이 파일 하나하나가 모두 모듈
- `모듈 번들러` : 이 웹 애플리케이션을 구성하는 몇십, 몇백개의 자원들을 하나의 파일로 병합 및 압축 해주는 동작

## [NPM](https://joshua1988.github.io/webpack-guide/build/node-npm.html#node-js%EC%99%80-npm)
- 자바 스크립트 프로그래밍 언어를 위한 패키지 관리자
- 전세계적으로 잘 쓰이는 자바스크립트 라이브러리(jquery, tenserflow, express..)를 가지고 있는 공개 저장소이다

<img src=https://joshua1988.github.io/webpack-guide/assets/img/webpack-bundling.e79747a1.png>
