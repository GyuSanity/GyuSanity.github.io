---
layout: post
title: 5. Vue.js 컴포넌트
category: Vue.js
tag: [Vue.js]
---

## Navigation Var

- ***[Vue Component 통신 방식](#vue-component-등록과-표시)***
- ***[Props 속성](#props-속성)***
- ***[Event Emit](#event-emit)***
- ***[같은 레벨의 컴포넌트간 데이터 전달 방법](#같은-레벨의-컴포넌트간-데이터-전달-방법)***

___

## [뷰 컴포넌트](https://joshua1988.github.io/vue-camp/vue/components.html)
- 컴포넌트는 화면의 영역을 구분하여 개발할 수 있는 뷰의 기능
- 컴포넌트 기반으로 화면을 개발하게 되면 코드의 재사용성이 올라가고 빠르게 화면을 제작 가능
- 제일 상위 Compoenet를 Root Component라고 부름
<img src="data:image/png;base64,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"> 

___

## Vue Component 등록과 표시

- 'Vue Application Instance Option 속성 또는 Option API에서 설정 가능
- Instacnce Option 속성 중 Components : 컴포넌트 이름 : 컴포넌트 내용으로 정의
- 정의된 Component들은 Html에 등록 필요


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
    <app-header></app-header>
    <app-footer></app-footer>
  </div>

  <div id="app2">
    <app-header></app-header>
    <app-footer></app-footer>
  </div>

  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

  <script>
    // 전역 컴포넌트
    // Vue.component('컴포넌트 이름', 컴포넌트 내용);
    
    Vue.createApp({
      data() {
        return {
          message: '10'
        }
      },
      components: {
        'app-header': {
          template: '<footer>app\'sheader</footer>'
        },
        'app-footer': {
          template: '<footer>app\'s footer</footer>'
        }
      }
    }).mount('#app');

    Vue.createApp({
      data() {
        return {
          message: '10'
        }
      },
      components: {
        'app-header': {
          template: '<footer>app2\'s header</footer>'
        },
        'app-footer': {
          template: '<footer>app2\'s footer</footer>'
        }
      }
    }).mount('#app2');
  </script>
</body>

</html>

```

___

## Vue Component 통신 방식

- Vue 컴포넌트는 Props와 이벤트(Emit)으로 통신함
- 각 컴포넌트는 고유한 데이터 유효 범위를 갖으며, 상위➡️하위 = Props, 하위➡️상위 = 이벤트(Emit)으로 정보를 주고 받음

<img src="https://joshua1988.github.io/vue-camp/assets/img/component-communication.2bb1d838.png">

___

## Props 속성

- props 속성을 사용하기 위해서 하위 컴포넌트에서 Props 속성을 정의하고, 상위 컴포넌트의 템플릿에도 코드 추가 필요
    ##### `하위컴포넌트` : props 속성 정의
    ##### `상위 컴포넌트 템플릿` : v-bind:프롭스 속성명=상위 컴포넌트의 데이터 속성 정의

```javascript
// 하위 컴포넌트의 내용
var childComponent = {
  props: ['프롭스 속성 명']
}
```

```html
<!-- 상위 컴포넌트의 템플릿 -->
<div id="app">
  <child-component v-bind:프롭스 속성 명="상위 컴포넌트의 data 속성"></child-component>
</div>
 + HTML에서는 대소문자를 구분하지 못해 '-' 표기 필요
```

ex.

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
    <!-- <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header> -->
    <app-header v-bind:propsdata="message"></app-header>
    <app-content v-bind:propsdata="num"></app-content>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var appHeader = {
      template: '<h1>{{ propsdata }}</h1>',
      props: ['propsdata']
    }
    var appContent = {
      template: '<div>{{ propsdata }}</div>',
      props: ['propsdata']
    }

    new Vue({
      el: '#app',
      components: {
        'app-header': appHeader,
        'app-content': appContent
      },
      data: {
        message: 'hi',
        num: 10
      }
    })
  </script>
</body>
</html>
```

___

## Event Emit
- 이벤트 발생은 컴포넌트의 통신 방법 중 하위 컴포넌트에서 상위 컴포넌트로 통신하는 방식
- 하위컴포넌트의 메서드 or 라이프사이클 훅에 이벤트 등록 + 상위 컴포넌트 템플릿에도 코드 추가 필요
    ##### `하위컴포넌트` : emit 이벤트 정의
    ##### `상위 컴포넌트 템플릿` : v-on:이벤트명=상위컴포넌트에서 실행할 메서드 or 연산

```javascript
// 하위 컴포넌트의 내용
this.$emit('이벤트 명');
```


```html
<!-- 상위 컴포넌트의 템플릿 -->
<div id="app">
  <child-component v-on:이벤트 명="상위 컴포넌트의 실행할 메서드 명 또는 연산"></child-component>
</div> 
```

ex.
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
    <p>{{ num }}</p>
    <!-- <app-header v-on:하위 컴포넌트에서 발생한 이벤트 이름="상위 컴포넌트의 메서드 이름"></app-header> -->
    <app-header v-on:pass="logText"></app-header>
    <app-content v-on:increase="increaseNumber"></app-content>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var appHeader = {
      template: '<button v-on:click="passEvent">click me</button>',
      methods: {
        passEvent: function() {
          this.$emit('pass');
        }
      }
    }
    var appContent = {
      template: '<button v-on:click="addNumber">add</button>',
      methods: {
        addNumber: function() {
          this.$emit('increase');
        }
      }
    }

    var vm = new Vue({
      el: '#app',
      components: {
        'app-header': appHeader,
        'app-content': appContent
      },
      methods: {
        logText: function() {
          console.log('hi');
        },
        increaseNumber: function() {
          this.num = this.num + 1;
        }
      },
      data: {
        num: 10
      }
    });
  </script>
</body>
</html>
```

___

## 같은 레벨의 컴포넌트간 데이터 전달 방법

```javascript
<!-- HTML -->
<div id="app">
  <app-header v-bind:app-title="message"></app-header>
  <app-contents v-on:login="receive"></app-contents>
</div>

<!-- JavaScript -->
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  var appHeader = {
    props: ['appTitle'],
    template: '<h1>{{ appTitle }}</h1>',
  }

  var appContents = {
    template: `
      <p>
        <button v-on:click="sendEvent">로그인</button>
      </p>
    `,
    methods: {
      sendEvent() {
        this.$emit('login');
      }
    }
  }

  // 루트 컴포넌트
  Vue.createApp({
    data() {
      return {
        message: ''
      }
    },
    methods: {
      receive() {
        console.log('받았다');
        this.message = '로그인 됨'
      }
    },
    components: {
      // '컴포넌트 이름': 컴포넌트 내용
      'app-header': appHeader,
      'app-contents': appContents
    }  
  }).mount('#app');
</script>
```
