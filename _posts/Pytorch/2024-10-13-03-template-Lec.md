---
layout: post
title: 3 머신러닝의 기본 개념, 학습의 동작 원리
category: DeapLearning
tag: [DeapLearning, pytorch]
---

## Navigation Var

- **[]()**

---

## 머신 러닝 개념

<img src="/public/img/PyTorch/Lec3/1.png">
- 이전에는 프로그래머가 규칙을 만들어서 개/고양이를 판단하도록 개입을 했으면,
- ML의 경우 모델과 데이터로 학습을 하여 `경험`을 갖추게 하는것

<img src="/public/img/PyTorch/Lec3/2.png">
- 예측이란 데이터(경험)을 바탕으로 지식을 습득하여 미래 발생할 일을 생각하는 것
- 데이터 분석 후 미래를 예견하는 forecast와 다름!
- 즉 ML에서 데이터가 매우매우 중요함

<img src="/public/img/PyTorch/Lec3/3.png">
- 머신러닝과 딥러닝의 차이점
  - `머신러닝` : 데이터가 들어왔을 경우 피처에 대한 전처리를 통해 넣어주는 것(고차원의 데이터가 아닌 저차원의 데이터들을 넣어줌. 피쳐가 잘 나눠지고 정제가 잘되는 작업에 유용함)
  - `딥러닝` : 고차원의 데이터를 정제없이 그냥 넣어 feature를 찾아내는 추세로 들어감. (Feature Extraction + Classification이 통합되어 합쳐짐)

<img src="/public/img/PyTorch/Lec3/4.png">
- 인공지능 모델을 사용하는 목표는 무엇인가? 즉 TASK는 무엇인가?
  - `분류(label)` : label을 생성(ex. 2진 분류)
  - `회귀(Regression)` : 연속형 값을 예측(ex. 가격 예측)
  - `생성(Generation)` : 입력 데이터로 부터 새로운 데이터 생성
  - 그외 것들도 Task들이 있으나 주로 분류에 대한 내용을 다룰 예정

<img src="/public/img/PyTorch/Lec3/5.png">
- 딥러닝의 파이프 라인은 데이터 -> 모델 -> feedback으로 모델 가중치를 업데이트 함
<img src="/public/img/PyTorch/Lec3/6.png">
- 조금더 자세히 들여다 보면, 입력 데이터를 준비하고 랜덤한 값으로 모델을 준비한 다음 학습을 시켜 각 이미지에 대한 예측값과 결과값을 비교하여 feedback을 주고, 딥러닝 모델의 대한 weigh를 업데이트하여 `최적화`를 수행. (SGD 최적화 기법이 있음)
- 이때 예측값과 결과값을 비교할때 `오차(Loss)`가 있으며 이를 보정하기 위한 feedback으로 최적화를 수행한다고 보면 됨

- 각 학습단계/추론단계 설명

<img src="/public/img/PyTorch/Lec3/7.png">
<img src="/public/img/PyTorch/Lec3/8.png">

---

## 머신 러닝 기본 원리

#### 데이터

<img src="/public/img/PyTorch/Lec3/9.png">
- 데이터의 경우 어떤 유용한 작업(TASK)를 하기 위해 수집된 좋은 데이터들이 이상적이다
- 좋은 데이터의 특징중 양/완결성/신뢰도는 만족하기 쉬우나,
- `시기적절함`은 만족하기 어려움
  - 예를 들어 사계절에 대한 예측을 수행한다고 할때 매년 겨울에 대한 데이터 값들이 달라지고 데이터 수집환경이 쉽지 않고 해당 환경 재현하기가 어려움. 또한 공장라인에서 데이터를 수집하려고 한다면 해당 기간동안 고장 라인이 효율적으로 돌아가기 어렵기 때문에 필요할떄 데이터를 수집하기 어려움. 따라서 이를 극복하기 위해 시뮬레이터를 만드는 작업도 요즘에 많이 이뤄지고 있음

<img src="/public/img/PyTorch/Lec3/10.png">
- 컴퓨터는 결국 수를 다루는 계산기 임으로 데이터를 숫자로 바꾸는 인코딩 작업이 입력데이터에 필요하며, 인코딩 후에는 벡터로 변환됨(특정 차원에 대한 값들로 `행렬`이라고 생각하면 됨)
- `딥러닝`에선 인코딩된 벡터를 `Tensor`로 다차원의 정보로 라고도 말하기도 함)차원에 따라 다르게도 말함)
  - 2차원 이상의 벡터 = Tensor로 딥러닝에선 말함

<img src="/public/img/PyTorch/Lec3/11.png">
- ML 에서는 주로 저차원 벡터를 사용하며,
- DL 에서는 주로 고차원 벡터를 사용함(2차원 이상의 전처리된 벡터 데이터 값을 다룸)

<img src="/public/img/PyTorch/Lec3/12.png">
- 입력 데이터에는 `멀티 모달 데이터`도 있음
  - `멀티 모달 데이터` : 입력으로 두개 이상의 유형 데이터를 사용하는 경우를 말함
- 멀티 모달 데이터로 학습하는 과정을 멀티모달 하습 이라고도 말하며, 최근 활발하게 연구되고 있는 분야중 하나임.

#### 모델

## <img src="/public/img/PyTorch/Lec3/13.png">

- 앞 딥러닝 데이터 파이프 라인에서 이야기 햇듯이,
  - 딥러닝의 경우, 데이터 -(전처리)-> 모델 -> 출력 -(오차계산)-> Model Update(Optimization)이라고 했었는데 이번에는 데이터 이후인 모델에 대해 좀더 자세히 보겠음

<img src="/public/img/PyTorch/Lec3/1.png">
<img src="/public/img/PyTorch/Lec3/1.png">
<img src="/public/img/PyTorch/Lec3/1.png">
<img src="/public/img/PyTorch/Lec3/1.png">
<img src="/public/img/PyTorch/Lec3/1.png">
<img src="/public/img/PyTorch/Lec3/1.png">
<img src="/public/img/PyTorch/Lec3/1.png">
<img src="/public/img/PyTorch/Lec3/1.png">
<img src="/public/img/PyTorch/Lec3/1.png">
