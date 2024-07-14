---
layout: post
title: "MarkDown 사용법"
category: MarkDown
tag: [MarkDown, VSCode]
---

# MarkDown 사용

## Markdown 이란
일반 텍스트 문서의 양식을 편집하는 문법이다.
MD를 통해 작성된 문서는 쉽게 HTML등 다른 형태의 문서로 쉽게 변환이 가능함

## Navigation Var
- **[HEADER표현](#HEADER표현)**
- **[수평선](#수평선)**
- **[라인개행](#라인개행)**
- **[LIST](#LIST)**
- **[문장강조](#문장강조)**
- **[인용](#인용)**
- **[링크삽입](#링크삽입)**
- **[이미지삽입](#이미지삽입)**
- **[이모지](#이모지)**
- **[각주](#각주)**


## HEADER표현
```
# 제목1
## 제목2
### 제목3
#### 제목4
##### 제목5
###### 제목6
```

## 수평선
```
---
```

## 라인개행
띄어쓰기 두번 입력

## LIST
```
1. 첫번째
1. 두번째
1. 세번째
  

+ 순서없음
  + WTF
    + I Don know who you are
      + Nice to meet you
```

## 문장강조
```
__볼드(진하게)__  
_이탤릭체(기울여서)_    
~~취소선~~  
<u>밑줄</u>  
__볼드로 진하게 만들다가*이탤릭으로 기울이고*다시 볼드로__(중복 활용도 가능하다.)
```

## 인용
```
> 인용
>> 인용2
>>> 인용3
```

>인용
>> 인용2
>>> 인용3

## 링크삽입
```
[문장](URL "말풍성")  
<URL>  
[문장](#TAG) <- 동일 파일내 문단 이동>
```

## 이미지삽입
```
유형1(`이미지` 삽입) :  
![이미지](https://theorydb.github.io/assets/img/think/2019-06-25-think-future-ai-1.png "인공지능")
  
유형2(`사이즈를 조절`하고 싶은 경우 HTML 태그로 처리) :   
<img src="https://theorydb.github.io/assets/img/think/2019-06-25-think-future-ai-1.png" width="300" height="200"> 

유형3(이미지 삽입 후, `링크 걸기`)
[![이미지](https://theorydb.github.io/assets/img/think/2019-06-25-think-future-ai-1.png)](https://theorydb.github.io/think/2019/06/25/think-future-ai/)
```

## 이모지
```
Window10 : 윈도우 키 + 마침표(.)
Mac : Command + Control + Space Bar
```

## 각주
```
Info[^Info]는 인용하는 부분이다

[^Info]: Information에 대한 설명이다.
```
Info[^Info]는 인용하는 부분이다

[^Info]: Information에 대한 설명이다.
