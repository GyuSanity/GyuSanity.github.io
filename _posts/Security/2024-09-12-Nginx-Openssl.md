---
layout: post
title: 1. HTTPS와 SSL 인증서
category: [Security]
tag: [OpenSSL, Nginx, Http/Https]
---

## Navigation Var

- **[HTTP vs HTTPS](#http-vs-https)**
- **[SSL 디지털 인증서](#ssl-디지털-인증서)**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**
- **[]()**

---

## HTTP vs HTTPS

- `HTTP(Hyper Text Transfer Protocol)` : HTML을 전송하기 위한 통신 규약
- `HTTPS(Hyper Text Transfer Protocol Security)` : 암호화된 HTML을 주고 받는 통신 규약으로 HTTP의 보안 규격을 강화하여 악의적인 감청이나 데이터 변동이 막기 위해 등장
  - `HTTPS = SSL?` : SSL 프로토콜 위에서 돌아가는 것이 HTTPS다.(웹 = 인터넷이긴 하나 인터넷 위에서 웹이 돌아가는것과 같음)
  - `SSL = TLS?` : 같은 말이다. 네스케이프에 의해 SSL 이 등장하였고 표준화 기구(IETF)의 관리로 변경되면서 TLS라는 이름으로 바뀜

---

## SSL 디지털 인증서

- 클라이언트와 서버간 통신을 제3자가 보증해주는 전자화된 문서(=공증)
  1. 클라이언트가 서버에 접속한 직후 서버는 클라이언트에게 이 인증서를 전달
  2. 클라이언트는 이 인증서를 신뢰할수 있는지 검증 후 다음 절차 수행
- `SSL/SSL 디지털 인증서 장점`
  1. 통신 내용 노출을 막음 (보안)
  2. 클라이언트가 접속하는 서버가 신뢰할만한지 판단(보증)
  3. 통신 내용의 악의적인 변경을 막음

---

## CA(Certificate Authority)

- 클라이언트가 접속하려는 서버가 맞는지 보장해주는 회사들을 말함(SSL 인증서를 발급해주는 제3자)
- CA 리스트는 브라우저가 가지고 있으며, 아래와 같이 구분

  - 공인 받은 CA가 발급한 SSL 인증서가 아닌 경우(사설기업 or 자체 서명한 인증서)
    <img src="/public/img/SSL/CA-x.png">
  - 공인받은 CA가 발급한 SSL 인증서일경우
    <img src="/public/img/SSL/CA-o.png">

  * 인증서가 포함하고 있는 정보들(공개키 + 서비스 정보)
    <img src="/public/img/SSL/Certificate.png">

---

## 암호화 종류

| 대칭키(=Session Key)                                                                                                              | 비대칭키(=공개키)                                      |
| --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| ![Session Key](/public/img/SSL/session.png)                                                                                       | ![Session Key](/public/img/SSL/private_public_key.png) |
| 하나의 키값으로 데이타(Text)를 암호화/복호화 <br> **장점** <br> \> 상대적으로 비대칭키보다 처리속도가 빠름 <br> \> 보안 역할 수행 |                                                        |
|                                                                                                                                   |                                                        |
|                                                                                                                                   |                                                        |
|                                                                                                                                   |                                                        |
|                                                                                                                                   |                                                        |

- SSL의 핵심은 암호화이며, SSL은 보안과 성능상의 이유로 2가지 암호화 기법을 혼용ㅇ해서 사용
  1. `대칭키` : 동일한 키값을 가지고 암호화/복호화 하는 방식

```bash
#암호화(인코딩)
// =>enc 수행시 비밀번호를 요구하는데 해당 비밀번호가 대칭키값이 됨
echo 'this is the plain text' > plaintext.txt;
openssl enc -e -des3 -salt -in plaintext.txt -out ciphertext.bin;
=> enc -e -des3 : des3 방식으로 암호화 함
=> -in plaintext.txt -out ciphertext.bin : plaintext.txt 파일을 암호화 한 결과를 ciphertext.bin 파일에 저장함

#복호화(디코딩)
openssl enc -d -des3 -in ciphertext.bin -out plaintext2.txt;
```

2. `공개키(비대칭키)` :

- ***

  ***

  ***

  ***

  ***

  ***

  ***

  ***

  ***

  ***

  ***

  ***

## REF

- 생활코딩 : [link](https://opentutorials.org/course/228/4894)
