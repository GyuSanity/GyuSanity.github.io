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

<img src=https://joshua1988.github.io/webpack-guide/assets/img/webpack-bundling.e79747a1.png>


## App Component
- app.vue에서 template/script/style 확인이 가능하며, HTML TAG 특성상 대소문자를 구분하지 못하여 파스칼 case로 작성하는 것을 추천함
- App.vue에서는 html/javascript/css 영역을 vue 싱글 파일 컴포넌트의 모습이며, javascript 영역에서 각 개별 싱글 파일 컴포넌트를 import 하여 하나의 거대한 컴포넌트 트리를 작성하는 것이다
- main.js에서는 작성된 싱글 파일 컴포넌트들의 주인이 되는 곳이며, public/index.html에 마운트 되어 홈페이지 렌더링을 수행
- javascript 속성 축약 문법에 의해서 컴포넌트는 아래와 같이 축약이 가능

```javascript
//컴포넌트이름 : 컴포넌트 내용
//'app-header' : AppHeader
//'AppHeader' : AppHeader
//AppHeader : AppHeader => 문자열을 괄호를 벗겨내도 동일
//AppHeader => Key/Value 값이 같을 경우 Javasciprt 속성 축약 가능

```


<details>

```javascripts

<!-- HTML 영역 -->
<template>
  <HelloWorld msg="welcome"/> #=> 파스칼 케이스로 작성하는 것을 추천
  <hello-world msg="welcome"></hello-world> #=> HTML TAG는 스펙상 대소문자 구분을 못함
</template>

<!-- JAVASCRIPT 영역 -->
<script>
// import 라이브러리 from '라이브러리이름'
import {{ vue }} from 'vue'
// import 컴포넌트이름 from './컴포넌트 경로'
import HelloWorld from './components/AppHeader.vue'

export default {
  // 인스턴트 옵션 속성 구분이 들어옴
  components: {
    // '컴포넌트이름': 컴포넌트 내용
    HelloWorld
  },
}
</script>

<!-- CSS 영역 -->
<style>
</style>

```
</details>

## 싱글 파일 컴포넌트 코드 작성 팁
- app.vue를 싹다 지운 후 아래와 같은 `vue vscode snippets`으로 코드 자동완성으로 수월하게 만들수 있음
- `vbc` : template/script/style 작성 가능
- `vdata` : data 속성을 자동완성, data(){ return {} } 
- `vmethods` : method 속성을 자동완성


## 싱글 파일 컴포넌트 props/evnet emit 실습
- 하위 컴포넌트 AppHeader 뷰에서 change 이벤트를 올릴 경우 상우 컴포넌트에서 해당 이벤트를 받아 message를 변경하고, 이를 다시 bind로 하위 컴포넌트한테 내려줌

<details>

```javasciprt
#####App.vue
<template>
  <AppHeader 
    v-bind:appTitle="message"       **=> message data를 appTitle Props로 내림
    v-on:change="changeMessage">    **=> Event의 경우 change emit으로 올라온 이벤트가 있을 경우 changeMessage 함수를 실행한다
  </AppHeader>
</template>

<script>
// import 컴포넌트이름 from './컴포넌트 경로'
import AppHeader from './components/AppHeader.vue'

export default {
  components: {
    // '컴포넌트이름': 컴포넌트 내용
    // 'app-header': AppHeader,
    // 'AppHeader': AppHeader,
    // AppHeader: AppHeader,
    AppHeader
  },
  data() {
    return {
      message: '앱 헤더 컴포넌트'
    }
  },
  methods: {
    changeMessage() {
      this.message = '변경됨'
    }
  }
}
</script>

<style scoped>

</style>


#####AppHeader.vue
<template>
  <h1>{{ appTitle }}</h1>
  <button @click="changeTitle">변경</button>
</template>

<script>
  export default {
    props: ['appTitle'],
    methods: {
      changeTitle() {
        this.$emit('change');
      }
    }
  }
</script>

<style scoped>

</style>

```

</details>


- 