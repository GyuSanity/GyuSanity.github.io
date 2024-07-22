---
layout: post
title: 7. Vue CLI 프로젝트 생성
category: Vue.js
tag: [Vue.js]
---

## Navigation Var

***[vuecli](#vuecli)***
***[vuecli 설치 및 실행](#vuecli-설치-및-실행)***
***[project 폴더 내용 살펴보기](#project-폴더-내용-살펴보기)***
***[vue실행결과확인하기](#vue-실행-결과-확인-하기)***

## VUECLI
- Vue.js로 주로 사용하는 프로젝트 생성 도구 ( 명령어로 프로젝트를 간단히 생성 가능)
- VueCLI 공식 문서에서 확인 가능


## Vuecli 설치 및 실행
- Install & crate project
```javascript
#install
npm install -g @vue/cli
or
yarn global add @vue/cli
#create project
vue create vue3-cli

#start
cd vue3-cli
yarn server => project 관련된 라이브러리 설치 (vue-cli-service serve, package.json에서 확인가능)
```

## Project 폴더 내용 살펴보기

- `package.json` : 이름/버전/커스텀스크립트(ex. yarn server), dependencies, devdependencies, eslint 설정등 확인 가능
    + `dependencies/devDependencies` : 배포용인지 개발용인지 차이며, npm i [lib, ex jquery]를 통해 설치되는 것이 dependencies이며, -d 를 붙이면 개발용 립으로 포함됨
    + 배포할때만 사용되는 라이브러리는 빌드 도구(webpack), 코드 문법 검사 도구(eslint), 이미지 압축도구(imagemin)등이 있음
- `vue.config.js` : Vue 프로젝트 Webpack 관련 설정 가능(Ctrl+space로 추가 가능)
    + [eslint 외 도움이 되는 개발 도구](https://joshua1988.github.io/web-development/vuejs/boost-productivity/)
- `public/index.html` : application 진입점 page(초기 보여주는 html 껍데기 파일), vue에서 작성한 프로젝트 결과물이 여기에 붙음

- `main.js` : Vue 어플리케이션 인스턴스 생성 밑 #app div tag에 마운트

```javascript
import { createApp } from 'vue' => dependencies에 설정된 lib 파일을 createApp으로 들고옴
# Vue.createApp(app).mount('#app')과 같은 형태로 뷰 라이브 러리를 들고옴

import App from './App.vue' => App.vue 뷰 파일을 App으로 들고옴 (CDN 형태가 아니라 npm 저장소에 있는 라이브러리를 프로젝트 node_modules 밑에 설치된 라이브러리를 가져온다)
# vue create vue3-cli를 수행시 npm i [] 를 자동으로 수행해주는 것이다.
createApp(App).mount('#app')

#즉 아래와 같이 vue로 인스턴스를 만든 후 createApp을 하는 형태와 같은 코드이다
var vue = {
    <template>
  <AppHeader 
    v-bind:appTitle="message"
    v-on:change="changeMessage">
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
}
createApp(App).mount('#app')
```

## Vue 실행 결과 확인 하기
- network pannel을 보면 순차적으로 요청된 순서들을 확인할수 있음.
- localhost 응답에는 app에는 아무 응답이 없는데 chunk-vender.js/app.js가 app 내용을 받아와 표현해주는 형태

__ref__. NPM 무료 강의 : [LINK](https://www.inflearn.com/course/lecture?ourseSlug=%ED%94%84%EB%9F%B0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%ED%8C%A9&unitId=37371)