---
layout: post
title: 1 인공지능의 역사, 인공지능의 기본 원리
category: DeapLearning
tag: [DeapLearning, pytorch]
---

## Ref

- [day1](1https://gyusanity.github.io/ai/2024/10/17/day1/)
- [day2](https://gyusanity.github.io/ai/2024/10/18/day2/)

## Navigation Var

- **[OT](#ot)**
- **[인공지능이란?](#인공지능이란)**
- **[학습의 개념](#학습의-개념)**
- **[학습 방법](#학습-방법)**

---

## OT

<img src="/public/img/PyTorch/Lec1/1.png">

## 인공지능이란?

<img src="/public/img/PyTorch/Lec1/2.png">
- 이미테이션 게임을 통해 인공지능에 대한 나오는데, 인간이 몇주나 걸리는 것을 기계해독으로 몇일로 해독하는 영화가 있음 이를 통해 등장되었는데 한번 기회되면 보면 좋을듯함

<img src="/public/img/PyTorch/Lec1/3.png">
- 인공지능 연구의 궁극적인 목표 알렌 튜닝에 의해 개발된 Turning Test를 통과하는 것임
- 예를 들어 사용자가 게임을 하고 있는데 이게 인공지능인지 사람인지 모를 정도의 테스트를 말함
- 인공지능에는 기계학습과 딥러닝이 있음
  - 기계학습(ML) : `데이터 학습을 통한 인공지능 시스템`
  - 딥러닝(DL) : `신경망 기반의 기계학습 일종`

<img src="/public/img/PyTorch/Lec1/4.png">
- 인공지능이 가장 포괄적인 개념으로 if-else만으로도 만들수 있는게 인공지능이고,
- 규칙을 과거의 데이터로 부터 배우는 것이 기계학습(Machine Learning) => Decision Tree(DT), Soft Vector Machine등을 2000년대 이전에 쓰였음
- 인간의 뇌 구조로 영감을 얻어 신경망(Neural Network)을 통해 만든 모델을 이용하여 인간처럼 학습하는 기계 => 현재 쓰이는 방법이며 현재 자연어처리나 비전처리에서 성과를 보이고 있음

---

## 학습의 개념

<img src="/public/img/PyTorch/Lec1/5.png">
- 데이터를 기반으로 학습하는 ML/DL이라고 하는데, 그럼 ML/DL에서 이 학습의 개념이 무엇인가? 이를 위해선 예측을 알아야함
- `예측` : 주어진 데이터의 경험을 바탕으로 지식을 습득하고, 이를 통해 미래의 발생할 일을 생각하는 것을 말함.
- 위의 예측은 날씨 예측과 같은 forcast와 다름(과거 데이터를 `분석`해서 미래를 예상), 딥러닝은 경험을 바탕으로 학습한 지식으로 미래를 예측하는 것임
- 개의 사진이 다양하게 있으면(distribution이 다양한 데이터) 이를 통해 지식이 확장되어 예측이 잘됨. 따라서 얼마나 많은 양의 데이터가 필요한가? 이에 대한 질문은 정형화 해서 이야기 할수 없고 모을수 있을 만큼 최대한 모아라...

<img src="/public/img/PyTorch/Lec1/6.png">
- 모델이란 데이터(X)를 통해 구하고자 하는 해답(a,b)을 말함
- supervised에 국한되서 모델을 설명하면, 데이터와 정답이 구해졌을때 기울기와 편향인 a,b를 구하는 것을 말함
- ax+b가 모델인 것이고, 이때 데이터(x)와 결과[y(f(x))]를 가지고 모델의 a/b 값을 구하는 것임
- 학습 파라미터는 기울기와 편향을 구하는 것인데 편향(절편)없고 기울기(a)를 구하는 경우도 있고, 둘다 구하는 경우도 있음 (aX+b, 4X+b).
- 기울기 편향이 다 정해진 경우(4X+2)는 추론을 한다고 말함

<img src="/public/img/PyTorch/Lec1/7.png">
- 학습을 하다보면 `결정경계`의 개념도 등장함.
- 결정경계(Decision boundary)란 y=ax+b라는 함수로 데이터를 잘 분류할 수 있는 직선을 찾는 다는 것을 말함.
- 선이 한개로 나타나는 경우는 선형 구분 가능이라고 하나 대부분은 선형으로 구분이 잘 안됨.

<img src="/public/img/PyTorch/Lec1/8.png">
- 결정 경계는 임의의 직선으로 부터 시작하며, 학습을 통해 좋은 직선을 찾게됨
- 다만 데이터 특성으로 복잡한 데이터의 경우 100%가 나오기 힘든 경우도 있다.

---

## 학습 방법

<img src="/public/img/PyTorch/Lec1/9.png">
- 데이터에 대해서 라벨이 있으면 `지도학습`,
- 데이터에 대해서 라벨이 없는 경우가 `비지도 학습(데이터의 분포만 가지고 찾는것)`
- 데이터에 대해서 action/reward를 통해서 rewards를 최대화 하는게 `강화학습`
- 데이터에 대해서 일정수의 라벨로 학습을 하고 이후 라벨이 없는 데이터로 검증/학습을 하는 것이 준지도학습

<img src="/public/img/PyTorch/Lec1/10.png">
<img src="/public/img/PyTorch/Lec1/11.png">
<img src="/public/img/PyTorch/Lec1/12.png">
- 손오공/베지터가 확실한 데이터로 학습 후 결정경계를 찾은 후에 분류하기 애매한 사진들로 검증/태스트하여 나머지들을 분류하는 것을 말함
<img src="/public/img/PyTorch/Lec1/14.png">
- 환경이 주어지고, 사용자가 action을 통해서 reward를 줌(바로 줄수도 있고 다 끝나고 주는 경우도 있음). 이를 통해 모델을 학습.

---
