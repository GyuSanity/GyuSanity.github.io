---
layout: post
title: TypeScript를 쓰는 이유
category: TypeScript
tag: [TypeScript]
---

## 목차
- [목차](#목차)
- [타입 스크립트란?](#타입-스크립트란)
  - [왜 타입스크립트를 사용하는가?](#왜-타입스크립트를-사용하는가)
  - [에러의 사전방지](#에러의-사전방지)
  - [코드 가이드 및 자동완성(개발성 향상)](#코드-가이드-및-자동완성개발성-향상)

__

## 타입 스크립트란?
타입 스크립트는 자바 스크립트에 타입을 부여한 언어이며, 자바스크립트의 확장된 언어라고 볼수 있다. 다만 타입스크립트는 자바 스크립트와 달리 브라우저에서 실행하려면 변환하는 컴파일 과정이 필요함

___

### 왜 타입스크립트를 사용하는가?
2가지 관점에서 기존 자바 스크립트의 코드의 품질과 개발 생산성을 높일 수 있음.
1. *에러의 사전방지*
2. *코드 가이드 및 자동완성(개발성 향상)*

___

### 에러의 사전방지
자바 스크립트의 경우, 아래와 같이 타입을 명시하지 않아 의도하지 않은 동작을 수행하는 경우가 있음
```
// math.js
function sum(a, b) {
  return a + b;
}

sum(10,20) // 30
sum('10', '20') // 1020 출력
```
타입스크립트의 경우, 아래와 같이 타입을 명시하여 의도하지 않은 동작을 사전에 예방할수 있음
```
// math.ts
function sum(a: number, b: number) {
  return a + b;
}
sum('10', '20'); // Error: '10'은 number에 할당될 수 없음
```
___

### 코드 가이드 및 자동완성(개발성 향상)
아래와 같이 total 변수로 값을 받을 경우 자바스크립트에서는 number라는 것을 인지하지 못하여 개발자가 스스로 sum() 함수의 결과를 number로 가정한 상태에서 toLocaleString을 코딩해야함

```
// math.js
function sum(a, b) {
  return a + b;
}
var total = sum(10, 20);
total.toLocaleString();
```

타입스크립트의 경우에는 변수 total에 인자 및 리턴값에 타입을 지정할수 있어서 자동완성(Tap)으로 확인시 number임을 알수 있으며 자동완성으로 정확하고 빠르게 작성해 나갈 수 있음
```
function sum(a: number, b: number): number {
  return a + b;
}
var total = sum(10, 20);
total.toLocaleString();
```
