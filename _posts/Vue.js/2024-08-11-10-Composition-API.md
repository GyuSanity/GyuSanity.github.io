---
layout: post
title: 10. Composition API 기초
category: Vue.js
tag: [Vue.js, compositionAPI]
---

## Navigation Var

- **[Composition API란?](#composition-api란)**
- **[Composition API 등장 배경](#composition-api-등장-배경)**
- **[Composition API Basic](#composition-api-basic)**
- **[Composition API 장점](#composition-api-장점)**
- **[Composition API 단점](#composition-api-단점)**

---

## Composition API란?

- 컴포넌트의 재사용성을 높여주는 것이 `Composition API` 이다
- Vue3에서만 지원하지 않고 Vue2에서도 Composition API를 지원하고 있음!

---

## Composition API 등장 배경

- React Hook이 등장한 후에 Funtion based Compoent API = `Composition API`를 논의함
- React와는 다르게 vue.js는 `Reactivity(반응성)`을 기반으로 화면을 업데이트하고, React는 `state` 변화가 감지되었을 때 컴포넌트/DOM을 업데이트하여 렌더링 하는 부분이 다름
- 아래와 같은 형태로 PR로 논의되었음
  https://github.com/vuejs/rfcs/pull/42
  https://github.com/vuejs/rfcs/pull/78
  https://github.com/vuejs/rfcs/blob/master/active-rfcs/0013-composition-api.md
  https://github.com/vuejs/rfcs/blob/function-apis/active-rfcs/0000-function-api.md

---

## Composition API Basic

- `setup 등장` : data와 methods를 따로 선언하는 것이 아니라 함꼐 선언하며, 꼭 return을 해야 setup 안에서 정의된 값들을 setup 밖에서 사용할수가 있음
- `ref 등장` : Reactivity를 주입하는 Lib을 활용하여 웹 페이지에 표현하고자 하는 값들에 대하여 반응성을 주입할수 있게됨
- 위 외에도 `Computed/Watch/Lifecyfcle/Props/Event Emit/script setup` API들도 같이 등장하여 문법적으로 사용하는 부분이 달라짐

```javascript
## 기존 Option API
<template>
  <div>
    <p>{{ message }}</p>
    <button @click="changeMessage">change</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: 'Hi'
    }
  },
  methods: {
    changeMessage() {
      this.message = 'Hello'
    }
  }****
}
</script>


## Composition API
<template>
  <div>
    <p>{{ message }}</p>
    <button @click="changeMessage">change</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const message = ref('Hello');
    const changeMessage = () => {
      message.value = 'Hi';
    }

    return { message, changeMessage }
  }
}
</script>


```

---

## Composition API 장점

- vue3로 넘어가면서 **typesciprt를 적용**하여 변수/함수 타입을 하도록 하여 setup 내에서 **타입 추론**이 용이해졌음
- **Destructuring 문법**으로 원하는 변수/함수를 꺼내 코드 함수 **재사용성을 높일수 있음**

<img src="/public/img/VueLecture/VuecompositionAPI.png">

- 재사용되는 변수/함수의 setup 부분을 hook/components에 빼두고 destructuring 문법으로 빼내와 사용 가능

\+ Destructuring Syntax

```javascript
onst obj = {
  a: 10,
  b: 'hi'
}

const result = obj.a; <--- 일반적으로 꺼내오는 방식
const { a } = obj;    <--- Destructuring 방식으로 원하는 변수를 바로 꺼내오는 방식임

```

---

## Composition API 단점

- 로직을 보기 위해선 분리되어 있는 소스 코드들을 보기에 직관적이지 않음( 소스 코드가 몇백줄 이상으로 복잡해질 경우에 나눠야 좋음)
- setup 내 `data/methods/computed`가 섞이게 되면서 어느 부분이 그에 상응하는지 판단하기 어려움

---

## REF

- more about Composition API : [VUE JS 공식 문서](https://vuejs.org/guide/extras/composition-api-faq.html)
- 수업 자료 : [인프런 웹 Page](https://joshua1988.github.io/vue-camp/reuse/composition.html)
