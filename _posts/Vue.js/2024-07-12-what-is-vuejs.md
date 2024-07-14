---
layout: post
title: Vue.js란?
category: Vue.js
tag: [Vue.js]
---

## Navigation Var
- **[Vue.js란](#Vue.js란)**
- **[Vue2,Vue3의 차이점](#Vue2,Vue3의-차이점)**
- **[WebPack](#WebPack)**
- **[LIST](#LIST)**
- **[문장강조](#문장강조)**
- **[인용](#인용)**
- **[링크삽입](#링크삽입)**
- **[이미지삽입](#이미지삽입)**

## Vue.js란?
- Progressive JavaScript FrameWork로서 간단한 화면 UI 개발, 라우팅[=페이지간 이동], SSR[^SSR] 등의 애플리케이션 레벨의 개발을 지원하는 프레임워크를 말함
- React와 더불어 실무에서 가장 많이 사용되는 FE(Front End) 개발 라이브러리이며, React에 비해 진입 장벽이 낮고 쉽게 배울 수 있음
- 개발 생산성이 높고 자바스크립트 지식이 크게 요구 되지 않음

## Vue2,Vue3의 차이점
- 라이브러리 내부 로직 재작성(=>타입스크립트로 변경됨)
- 주요 개발 도구들 변경
  - ex. Vue 개발자 도구, VScode 플러그인, Vite 기반 프로젝트 생성
- 옵션 API -> Composition API 등장, Teleport등 새로운 문법 지원
- Reactivity System 기반 API 변경
- 공식 문서 변경
  - [vue2](https://v2.vuejs.org)
  - [vue3](https://vuejs.org)

+__reference__ : [vUE3로 넘어가면서..](https://joshua1988.github.io/web-development/vuejs/vue3-coming/)

## WebPack
- WebPack이란 FE 프레임워크에서 가장 많이 사용되는 모듈 번들러이며, 여러개의 파일(모듈)로 나누어 개발한 코드를 하나의 파일(or Chunk)로 묶어 주는 도구를 말함.
- 위에서 말하는 여러개의 모듈 = 웹 애플리케이션을 구성하는 자원(HTML/CSS/JS/Image 등)  


Vue 프로젝트에서는 Webpack을 아래와 같은 이유로 사용함.
1. 자바 스크립트의 변수 유효 범위 문제 해결
2. 브라우저별 HTTP 요청 숫자의 제약해소(번들링으로 묶어서 HTTP 요청 횟수를 줄일수 있음)
3. Dynamic Loading / Lazy Loading 미지원 ( 원하는 모듈을 원하는 타이밍에 로딩할수 있음)

__Reference__ : https://joshua1988.github.io/webpack-guide/webpack/what-is-webpack.html
- 웹 개발시 사이트의 로딩 속도를 높이기 위해 많은 노력들이 있었음.
  1.__요청 횟수/크기 줄이기__ : 웹 태스크 매니저들을 이용해 파일들을 압축하고 병합하여 서버로 요청하는 파일의 숫자 줄이기
  2.__필요자원미리 로딩__ : 로딩 속도를 높이기 위해 필요한 자원들은 나중에 요청하는 Lazy Loading
- 웹 팩의 경우에는 필요한 자원은 미리 로딩하는게 아니라 그때 그때 요청하는 철학으로 탄색

## Vue 코드 작성 방법
옵션 API / 컴포지션 API 방식이 있음

- __옵션 API__
    destructing이 없어 초기 입문자가 보기 좋을 수 있음
    createApp 인스턴스 옵션 설정이 data가 있음
```javascript
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app">{{ message }}</div>

<script>
  const { createApp } = Vue

  createApp({
    data() {
      return {
        message: 'Hello Vue!'
      }
    }
  }).mount('#app')
</script>
```

- __컴포지션 API__
    컴포넌트 코드를 많이 사용하며 clean 코드를 지향하는 방식
    createApp 인스턴스 옵션 설정에 setup이 있음
```javascript
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app">{{ message }}</div>

<script>
  const { createApp, ref } = Vue

  createApp({
    setup() {
      const message = ref('Hello vue!')
      return {
        message
      }
    }
  }).mount('#app')
</script>
```

***

[^SSR]: Server Side Rendering, https://joshua1988.github.io/vue-camp/nuxt/ssr.html