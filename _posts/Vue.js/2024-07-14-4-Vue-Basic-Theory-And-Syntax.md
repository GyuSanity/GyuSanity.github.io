---
layout: post
title: 4. Vue.js 기본 개념 및 문법
category: Vue.js
tag: [Vue.js]
---

## Navigation Var

- **[기본 vue application](#기본-vue-application)**
- ***[vue application instance 속성 api들](#vue-application-instance-속성-api들)***
- **[vue project 유용한 기능](#vue-project-유용한-기능)**
- **[derective](#derective)**

## 기본 Vue Application

- `Vue Application Instance` : Vue 개발을 시작할때 기본으로 생성하는 인스턴스

- Vue2에선 `Vue Instance`이지만 Vue3에서는 `Vue Application Instance`로 변경

- `vue application instance`를 아래와 같이 생성 후 화면의 영역 중 어느 부분에 적용할지 `mount`를 수행

```javascript

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<body>
  <div id="app">
    
  </div>
</body>

<script>
  // Vue 2
  new Vue({
    el: '#app'
  })

  new Vue({
    // el: '#app'
  }).mount('#app') 

  // Vue 3
  Vue.createApp({
    data() {
      return {
        message: '10'
      }
    }
  }).mount('#app');
</script>

```

## Vue Application Instance 속성, API들

- `el` : 인스턴스가 그려지는 화면의 시작점 __(특정 HTML 태그, Vue2에서만 사용하며 Vue3에선 mount로 대체)__
- `template` : 화면에 표시할 요소 (HTML, CSS 등)
- `data` : 뷰의 반응성(Reactivity)이 반영된 데이터 속성
- [`methods`]() : 화면의 동작과 이벤트 로직을 제어하는 메서드
- `created` : 뷰의 라이프사이클과 관련된 속성
- `watch` : data에서 정의한 속성이 변화했을 때 추가 동작을 수행할 수 있게 정의하는 속성
- `derective` : method를 호출하기 위해서 `v-`가 붙은 HTML attribute를 말함

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <div id="app">
    <button v-on:click="logText">click me</button>
    <input type="text" v-on:keyup.enter="logText">
    <button>add</button>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    new Vue({
      el: '#app',
      methods: {
        logText: function() {
          console.log('clicked');
        }
      }
    })
  </script>
</body>
</html>
```

## Vue Project 유용한 기능

- `Vue VSCode Snippets` : 사용 시 `vbs`, `vdata`, `vmethod`로 기본 양식들을 자동완성하여 작성 가능

## derective
> [Official Docs](https://vuejs.org/api/)

- UI 개발을 할때 추가적인 JavaScript 코드를 작성하지 않고 사용할수 있도록 함
    - `v-if`
    - `v-else`
    - `v-for` : 배열을 순회하는 문법 제공

```javascript
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<body>
  <div id="app">
    <ul>
      <li v-for="item in items">{{ item }}</li>
    </ul>
  </div>

  <script>
    Vue.createApp({
      // 컴포넌트 옵션 속성
      data: function () {
        return {
          items: ['삼성', '인프런', '네이버'],
        };
      },
    }).mount('#app');
  </script>
</body>
```

    - `v-bind`
    - `v-on` 

__reference__

- [인스턴스 옵션](https://joshua1988.github.io/vue-camp/vue/instance.html#%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%86%AB%E1%84%89%E1%85%B3-%E1%84%89%E1%85%A2%E1%86%BC%E1%84%89%E1%85%A5%E1%86%BC)
- [Method 속성](https://joshua1988.github.io/vue-camp/syntax/methods.html)