---
layout: post
title: 3. Vue.js Reactivity 동작 원리
category: Vue.js
tag: [Vue.js]
---

## Navigation Var

- **[Reactivity-Proxy API](#reactivity-proxy-api)**
- **[reactivity vue2/3 차이점](#reactivity-vue23-차이점)**


## Reactivity-Proxy API

- Proxy : Data라는 객체를 모방한 다음에 해당 내용에 접근(get/set)에 대한 동작을 정의할수 있음
- Proxy Docs : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Proxy ( 구글링 시 MDN을 붙여서 구글링하면 됨)
- Console 창에 app 입력 시 Proxy 객체로 정의됨이 확인 가능하며, app.message = 'Hi'를 입력시 Hi 확인 가능
    data 객체 message 값 set일 경우 proxy이 set()을 호출하며, 이때 DOM으로 쿼리 셀렉터로 div 태그에 접근하여 HTML Msg 값을 갱신

- ___객체의 내용이 변하면서 렌더링되면서 화면에 표현되는 것을 Reactivity라고 하며 Vue에서 추구하고 있음___

```javascript
<div id="app">
  <!-- 여기에 뭐가 렌더링 된다. -->
</div>

<script>
  var data = {
    message: 10,
    num: 20,
  }

  function render(sth) {
    var div = document.querySelector('#app');
    div.innerHTML = sth;
  }

  var app = new Proxy(data, {
    get() {
      console.log('값 접근')
    },
    set(target, prop, newValue) {
      console.log('값 갱신')
      target[prop] = newValue;
      render(newValue);
    }
  })
</script>
```
___

__reference__

[Vue2 Reactivity](https://v2.vuejs.org/v2/guide/reactivity.html)

[Vue3 Reactivity](https://vuejs.org/guide/extras/reactivity-in-depth.html#what-is-reactivity)

___

## Reactivity Vue2/3 차이점
 - Vue2의 경우 Object oriented property(Object.defineProperty)를 사용할 경우 객체의 특정 속성에 대한 값만 을 정의하여 모든 속성에 대한 defineProperty를 수행해야하는 단점이 있었음

```JavaScript
var data = {
    a:10,
    b:20,
}
Object.defineProperty(data, 'b',{
    get(){

    },
    set(){

    },
});
```

- Vue3는 객체를 mock하여 어떤 속성이 들어오건 동일한 proxy API로 엮어 낼 수가 있음.

___