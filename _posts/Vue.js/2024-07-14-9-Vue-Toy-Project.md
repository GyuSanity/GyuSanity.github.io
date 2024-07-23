---
layout: post
title: 9. Toy Project(Login Page)
category: Vue.js
tag: [Vue.js]
---

## Navigation Var
***[toy project(프로젝트 생성 및 로그인 폼 UI 구성)](#toy-project프로젝트-생성-및-로그인-폼-ui-구성)***
***[v model 속성 및 동작 원리](#v-model-속성-및-동작-원리)***


## Toy Project(프로젝트 생성 및 로그인 폼 UI 구성)
- Vue CLI 프로젝트 생성
   
```javascript

vue create vue-toy-project
cd vue-toy-project
yarn server
```
- App.vue에 기본 폼 작성

- `v-on:submit="이벤트"` : form 태그 안에서 엔터 혹은 버튼 클릭이 생길 경우 submit으로 해당 이벤트를 잡아 낼 수 있음(제출 시 업데이트 되는 것을 막고자 한다면 method에 prevent 또는 vue submit 옵션에 적용 가능)

- `axios` :  JavaScript를 사용하여 HTTP 요청을 만드는 데 사용되는 라이브러리

- `jsonplaceholder` : 개발자가 API를 테스트하거나 프론트엔드 코드를 실습할 수 있도록 무료로 제공되는 가짜 온라인 REST API

- ___`submit`___ 을 누를 경우,
  - Network Tap's Header users/ stats 201 Type xhr(Xml Http Request, 자바스크립트에서 데이터를 요청하기 위한 하나의 타입)의 POST가 정상적임을 확인할수 있음
  - Network Tap's Payload에 어떤 값들이 실려가는지 확인 가능

<details>

```javascript

<template>
  <form action="" @submit.prevent="submitForm">
    <div>
      <label for="userId">ID:</label>
      <input id="userId" type="text" v-model="username">
    </div>
    <div>
      <label for="password">PW:</label>
      <input type="text" v-model="password">
    </div>
    <button type="submit">로그인</button>
  </form>
</template>

<script>
import axios from 'axios'
import { ref } from 'vue';

  export default {
    setup() {
      // data
      var username = ref('');
      var password = ref('');

      // methods
      var submitForm = () => {
        axios.post('https://jsonplaceholder.typicode.com/users/', {
          username: username.value,
          password: password.value
        }).then(response => {
          console.log(response);
        })
      }
      
      return { username, password, submitForm }
    },
    // methods: {
    //   logText() {
    //     this.pas <----- return 된 값들은 다른 곳에서 사용가능
    //   }
    // }

    // data() {
    //   return {
    //     username: '',
    //     password: '',
    //   }
    // },
    // methods: {
    //   submitForm() {
    //     // event.preventDefault(); <------ vue에서 submit 이벤트 업데이트를 막도록 문법을 제공함
    //     const data = {
    //       username: this.username,
    //       password: this.password,
    //     }
    //     axios.post('https://jsonplaceholder.typicode.com/users/', data)
    //       .then(response => {
    //         console.log(response)
    //       });
    //     // console.log('제출됨')
    //   }
    // }
  }
</script>

<style scoped>

</style>

```
</details>

## v-model 속성 및 동작 원리

#### v-model 속성
- `v-model` : input box(FORM 요소)에 있는 것을 vue data에 엮고 싶을때 쓰는 디렉티브

```javascript

<input v-model="inputText">
new Vue({
  data: {
    inputText: ''
  }
})
```

#### v-model 동작 원리

- `v-model`은 `v-bind`와 `v-on`의 기능 조합으로 동작하나 사용자가 일일이 이 두 속성을 지정하지 않고 좀 더 편하게 개발할수 있도록 고안된 문법

- 위 `v-model`을 아래와 같이 `v-bind`와 `v-on` 조합으로도 동작하며 아래와 같은 3가지 사실이 있음

  - v-bind 속성은 뷰 인스턴스의 데이터 속성을 해당 HTML 요소에 연결할 때 사용한다.
  - v-on 속성은 해당 HTML 요소의 이벤트를 뷰 인스턴스의 로직과 연결할 때 사용한다.
  - 사용자 이벤트에 의해 실행된 뷰 메서드(methods) 함수의 첫 번째 인자에는 해당 이벤트(event)가 들어온다.
  
`
❕한글 입력의 경우 한글자가 입력이 끝나야 v-model의 엮인 값 데이터가 업데이트가 되어서 한글의 경우 `v-bind`와 `v-on`으로 쓰는 것을 권고함
`

```javascript

<input v-bind:value="inputText" v-on:input="updateInput">

new Vue({
  data: {
    inputText: ''
  },
  methods: {
    updateInput: function(event) {
      var updatedText = event.target.value;
      this.inputText = updatedText;
    }
  }
})

```

- HTML 입력 요소 종류에 따른 v-model의 속성
(1) input 태그에는 `value / input`
(2) checkbox 태그에는 `checked / change`
(3) select 태그에는 `value / change`



__ref__ : [v-model 동작 원리 및 활용 방법](https://joshua1988.github.io/web-development/vuejs/v-model-usage/)

