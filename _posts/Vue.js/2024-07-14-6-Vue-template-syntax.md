---
layout: post
title: 6. 템플릿 문법
category: Vue.js
tag: [Vue.js]
---

## Navigation Var

***[템플릿 문법](#템플릿-문법)***
***[데이터 바인딩](#데이터-바인딩)***
***[디렉티브](#디렉티브)***
***[v-if / v-show 디렉티브 예제](#v-if--v-show-디렉티브-예제)***
***[v-for 디렉티브 예제](#v-for-디렉티브-예제)***
***[v-bind(Vue Data Binding) 예제](#v-bindvue-data-binding-예제)***

## [템플릿 문법](https://joshua1988.github.io/vue-camp/vue/template.html)

- 뷰의 템플릿 문법이란 화면을 조작하는 방법을 의미
- 크게 데이터 바인딩과 디렉티브로 나뉨
- 컴포넌트 단위로 개발을 진행할 때 각각의 화면 개발을 쉽게 도와줄수 있는 문법을 학습

___

## 데이터 바인딩

- 뷰 인스턴스에서 정의한 속성들을 화면에 표시하는 방법
- 가장 기본적으로 콧수염 괄호(Mustach Tag)가 사용됨

```javascript
<div>{{ message }}</div>
 
 Vue.createApp({
  data() {
    return {
      message: 'Hello Vue.js'
    }
  }
})
```
___

## 디렉티브

- 뷰의 화면 요소를 더 쉽게 조작하기 위한 문법이며, 리엑트에선 제공하지 않음
- 자주 사용되는 방식들을 모아 디렉티브 형태로 제공
- `v-`가 붙어있는 특별한 속성들을 말함
    `v-if` : 조건부 렌더링시 사용(`v-else-if/v-else`도 있음)
    `v-show` : 마찬가지로 조건부 렌더링시 사용(true일때만 렌더링)
        ___v-if랑 다른점___ : v-if는 태그 자체를 랜더링 하지 않지만 v-show는 렌더링하되 display:none 처리를 함으로 새로고침을 많이 하는 페이지일 경우 v-if 보다는 v-show가 더 적절함(매번 태그를 지웠다 그렸다하는건 부담이 될수도 있음)
    `v-for` : 배열 기반으로 리스트를 렌더링할때 사용(흔히 list tag랑 같이 사용)
    `v-bind(:)` : 태그의 속성을 데이터로 지정할떄 사용. 자식 컴포넌트에서 프롭스를 엮은 후 부모 컴포넌트에서 데이터를 내릴 때 사용(축약형 = `:` )
    `v-on(@)` : 이벤트 제어 디렉티브. 자식 컴포넌트에서 부모 컴포넌트로 올라오는 이벤트 catch or 클릭 이벤트 등에 사용(축약형 = `@`)

___


## v-if / v-show 디렉티브 예제

```javascript
<!-- HTML -->
<div id="app">
  <!-- 1. v-if -->
  <p v-if="login">로그인 되었습니다</p>
  <p v-else>로그인 하세요</p>
  <button v-on:click="loginUser">로그인</button>

  <hr>

  <!-- 2. v-show -->
  <p v-show="login">로그인 되었습니다</p>
  <button v-on:click="loginUser">로그인</button>
</div>

<!-- JavaScript -->
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  Vue.createApp({
    data() {
      return {
        login: false
      }
    },
    methods: {
      loginUser() {
        this.login = !this.login;
      }
    }
  }).mount('#app');
</script>
```

___

## v-for 디렉티브 예제

```javascript
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<div id="app">
  <h1>장 볼 리스트</h1>
  <ul>
    <li v-for="item in list">{{ item }}</li>
  </ul>
</div>

new Vue({ 
  el: "#app", 
  data: {
    list: ['소갈비', '감자', '당근', '무', '깐 밤', '소갈비찜 양념']
  }
})
```

___

## v-bind(Vue Data Binding) 예제
-  Tag(id/class/style..)등의 Attribute 내용을 model의 데이터를 연결할때 사용
- `<div class="primay">데이터 바인딩 예제</div>` 를 아래와 같이 v-binding으로 동적으로 사용 가능

```javascript
<style>
.primary {
  color: coral;
}
</style>

<!-- HTML -->
<div id="app">
  <!-- class 바인딩 -->
  <h1>클래스 바인딩</h1>
  <div :class="textClass">데이터 바인딩 예제</div>

  <!-- id 바인딩 -->
  <h1>아이디 바인딩</h1>
  <section :id="sectionId" :style="sectionStyle">
    반갑습니다.
  </section>
</div>

<!-- JavaScript -->
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  Vue.createApp({
    data() {
      return {
        textClass: 'primary',
        sectionId: 'tab1',
        sectionStyle: { color: 'red' }
      }
    }
  }).mount('#app');
</script>
```

___