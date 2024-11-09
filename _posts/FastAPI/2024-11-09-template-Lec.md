---
layout: post
title: 1. FASTAPI
category: FASTAPI
tag: [FASTAPI, BACKEND]
---

## Navigation Var

- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**

---

## 개발환경 설정

###### Python 가상 환경 구축

Mac
python -m venv example (가상 환경 생성)
cd example (example directory 이동)
source bin/activate (가상 환경 활성화)
Windows
python3.10 -m venv example (가상 환경 생성)
cd example (example directory 이동)
Scripts\activate.bat (가상 환경 활성화)

###### Docker Desktop 설치

Mac
https://docs.docker.com/desktop/install/mac-install/
Windows
https://docs.docker.com/desktop/install/windows-install/

###### PyCharm 설치

Mac
https://www.jetbrains.com/pycharm/download/#section=mac
Windows
https://www.jetbrains.com/pycharm/download/#section=windows

---

## FastAPI란?

- 최근(2018년말)에 만들어진 파이썬 기반 웹 프레임워크로 단기간 내에 많은 인기를 얻음[link](https://star-history.com/#tiangolo/fastapi&Date)
- 이전에 장고가 있어서 차이점은 다음과 같음
  - 장고
    - Battery Included 전략을 사용해서 프레임워크에서 기본적으로 제공해주는 기능이 많이 들어가 있음(초기 프로젝트 셋팅에 필요한 기능들이 추가되있으나 필요없는 기능들도 들어가있을수 있음)
    - 장고 REST 프레임워크인 `DRF`와 함께 많이 사용할수 있으며 MVC 패턴을 쉽게 구현할수 있으며 내장된 시리얼라이저를 활용하여 Validation 체크를 빠르게 할수 있음
    - DRF와 결합성이 강해 다른 프레임워크랑 호환성이 떨어짐
    - admin과 같이 기본적으로 제공하는 기능을 사용하여 빠르게 프로토타입을 제작하기 용이함
  - FastAPI
    - 경량 Framework로써 웹 프레임워크를 운영하는데 필요한 최소한의 기능만 들어가 있음
    - 개발자가 자신의 요구에 맞게 디자인 패턴을 적용하기 용이함
    - 비동기 처리를 프레임 워크 내 자체에서 지원하기 떄문에 장고 보다 성능이 우수함
    - 기능이 단순한 가벼운 웹서버를 만들거나 직접 디자인 패턴을 적용하여 확장가능한 어플리케이션을 만들고자 할떄 용이함

---

## FastAPI 장점

- 경량화 프레임워크라 성능이 우수함
- 직관적인 디자인
  - path/query/body/response/dependency 처리가 직관적임
- Type Hints를 지원
  - Pydantic (안정적인 타입 처리가 용이함)
  - Datavalidation
  - IDE Support
- 비동기처리
- 자동 API 문서 생성
  - OpenAPI 스펙에 맞는 API 문서를
  - SwaggerUI를 통해 웹서버에 실제 요청을 보내볼 수도 있음

---

## 웹서버 개발 필수 필요 지식

- 클라이언트-서버 모델
  - 서비스를 사용하는 요청자와 서비스를 제공하는 제공자를 나눠둔 모델
  - 역할과 책임을 각각 관리할수 있어 다음과 같은 장점이 있음
    - 확장가능성 : 하나의 서버에서 다수의 클라이언트 대응 가능
    - 관심사의 분리 : 역할을 분리해서 성능/보안에 대한 최적화 가능
- 웹서비스
  - HTTP 요청 : 클라이언트 ->(네트워크) -> 서버
  - HTTP 응답 : 클라이언트 <-(네트워크) <- 서버
  - API : 클라이언트/서버 올바르게 데이터를 주고 받기 위해 사전에 정의된 통신

---

## API란?

- Application Programming Interface : 서버의 기능을 클라이언트가 사용할수 있도록 제공해주는 인터페이스이다
  - 인터페이스는 기능을 외부에서 사용할수 있게 제공하는 것이며,
  - 예를 들어, 사용자가 에어컨을 사용하고자 할 경우 리모컨으로 다 조작이 가능함
  - 에어컨 내부는 어떻게 동작하는지는 모르고 껏다 켯다를 리모컨을 통해 통신이 가능

---

## API를 디자인하는 방법 RESTful API (=RESTAPI)

- Representational State Transfer
  - API를 설계하는 스타일 가이드 중 가장 많이 사용하는 방법 중 하나임
  - 서버에서 관리하는 데이터의 상태가 표현되는 디자인으로 클라이언트와 서버가 서로 예측 가능한 형태로 통신이 가능
  - 특징
    - 리소스와 메서드를 통해 표현됨
      - 리소스 : URL을 통해 고유한 리소스 표현
        - ex. /api/v1/posts 를 통해 해당 리소스에 접근 가능
      - 메서드 : Http Method를 통해 API 동작 표현
        - ex. (CRUD가 있음)
        - POST /api/v1/post -> post 생성(Create)
        - GET /api/v1/posts -> posts 조회(Read)
        - PATCH /api/v1/posts/123 -> post 수정(Update)
        - DELETE /api/v1/posts/123 -> post 삭제(Delete)

--

## Todo 서비스 만들기 (실습)

- 5가지 API를 만들어 실습 진행 예정 [Repo](https://github.com/GyuSanity/FastAPI)
  - GET
    - 전체 Todo 조회 : /api/v1/todos
    - 단일 Todo 조회 : /api/v1/todos/<id>
  - POST
    - ToDo 생성 : /api/v1/todos
  - PATCH
    - Todo 수정 : /api/v1/todos/<id>
  - DELETE
    - Todo 삭제 : /api/v1/todos/<id>
- 위 실습을 통해 기본적인 FastAPI를 학습하고 발전 시켜 나가볼꺼임

\+ 최종 완성본 Repo : [Link](https://github.com/qu3vipon/inflearn-todos)

## 프로젝트 구성 및 실행

- [Repo](https://github.com/GyuSanity/FastAPI)의 README.md 확인
- OpenAPI로 API 문서 확인 : http://127.0.0.1:8800/docs

--

##

--

##

--
