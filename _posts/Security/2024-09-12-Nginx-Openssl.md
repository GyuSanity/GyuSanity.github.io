---
layout: post
title: 1. HTTPS와 SSL 인증서
category: [Security]
tag: [OpenSSL, Nginx, Http/Https]
---

## Navigation Var

- **[HTTP vs HTTPS](#http-vs-https)**
- **[SSL 디지털 인증서](#ssl-디지털-인증서)**
- **[CA(Certificate Authority)](#cacertificate-authority)**
- **[암호화 종류](#암호화-종류)**
- **[SSL 동작 방식 (대칭키/비대칭키 둘다 사용)](#ssl-동작-방식-대칭키비대칭키-둘다-사용)**
- **[Openssl을 활용한 인증서 발급 및 Nginx 적용](#openssl을-활용한-인증서-발급-및-nginx-적용)**
- **[REF](#ref)**

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

| 대칭키(=Session Key)                                                                                                                                                                                                                                                                                                                                                                                    | 비대칭키(=공개키)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Session Key](/public/img/SSL/session.png)                                                                                                                                                                                                                                                                                                                                                             | ![Session Key](/public/img/SSL/private_public_key.png)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| 하나의 키값으로 데이타(Text)를 암호화/복호화 <br> **장점** <br> \> 상대적으로 비대칭키보다 처리속도가 빠름 <br> \> 보안 역할 수행 <br> **단점** <br> \> 양쪽다 키 확보를 위한 키 분배가 필요하며 보안에 취약함 <br> **활용** <br> 서버-클라이언트간 대칭키(세션키) 생성 후 보안 시 활용 <br> **`보안`** : 서버-클라이언트 간 데이터를 주고 받을 경우 대칭키 방식을 활용하며 암호화된 데이터를 주고 받음 | 두개의 키(public/private)를 만들어 public은 암호화, private은 복호화하는데 사용(반대로 private를 암호화, private을 복호화 하는데 사용도 가능) <br> **장점** <br> \> 상대적으로 대칭키보다 처리속도가 느리나 키 분배 과정이 필요 없음 <br> \> 보안/보증의 역할을 수행 가능 <br> **단점** <br> \> 상대적으로 대칭키보다 처리속도가 느림 <br> **활용** <br> 서버측에선 2개의 키를 private key/public key를 생성 후 보안/보증 시 활용 <br> **`보안`** : 서버측에서 public키를 클라이언트 측에 전달하며, 클라이언트 측은 보낼 데이터가 있을 경우 서버측 public key를 암호화 하여 전송. 서버측은 받은 암호화된 데이터를 private key 를 사용하여 복호화를 수행하여 **서버 클라이언트간 주고 받는 데이터가 노출되지 않음(보안)** <br> **`보증`** : 서버측에서 private key로 암호화된 인증정보 + 공개키를 클라이언트에 전달하며(SSL 인증서), 클라이언트측은 공개키로 복호화를 수행하여 서버측이 **신뢰할수 있는 사이트 인지 판단** ( private key로 암호화된 정보를 쌍이 되는 공개키로 복호화가 된다면 해당 서버는 CA에서 공즈을 해준 신뢰할수 있는 사이트임 ) |

---

- 대칭키와 공개키를 활용한 암호화 복호화

```bash
## 대칭키
#암호화(인코딩)
// =>enc 수행시 비밀번호를 요구하는데 해당 비밀번호가 대칭키값이 됨
echo 'this is the plain text' > plaintext.txt;
openssl enc -e -des3 -salt -in plaintext.txt -out ciphertext.bin;
=> enc -e -des3 : des3 방식으로 암호화 함
=> -in plaintext.txt -out ciphertext.bin : plaintext.txt 파일을 암호화 한 결과를 ciphertext.bin 파일에 저장함

#복호화(디코딩)
openssl enc -d -des3 -in ciphertext.bin -out plaintext2.txt;

## 공개키
#암호화(인코딩)
//=> 비공개/공개키 생성
openssl genrsa -out private.pem 1024;
openssl rsa -in private.pem -out public.pem -outform PEM -pubout;
echo 'coding everybody' > file.txt
openssl rsautl -encrypt -inkey public.pem -pubin -in file.txt -out file.ssl;

#복호화(디코딩)
openssl rsautl -decrypt -inkey private.pem -in file.ssl -out decrypted.txt

```

## SSL 동작 방식 (대칭키/비대칭키 둘다 사용)

> 서버와 클라이언트간 통신 수행시 `Handshake > Transfer > Session Terminate` 순으로 이루어짐

1. HandShake
   1. Clinet Hello
      1. 초기 클라이언트가 서버측 HTTPS 접근 단계를 말함
      2. 클라이언트측은 랜덤 데이터 + 지원하는 암호화방식 + 세션 ID를 서버한테 전달
   2. Server Hello
      1. 클라이언트에 대한 응답 단계
      2. 서버측에서 랜덤데이터 + 서버측에서 선택한 암호화 방식 + 인증서(public key + 서비스 정보) 전달
   3. 클라이언트측은 브라우저 내 CA 리스트들을 보며 인증서가 CA의해 발급됬는지 확인(**신뢰할수 있는 사이트인지 확인**)
      1. 서버측에서 제공받은 public key를 가지고 서비스 정보를 복호화 수행. 복호화가 성공한다면 이는 CA에서 발급한 인증서임을 알수 있음
      2. 클라이언트는 클라이언트에서 생성한 랜덤 데이터 + 서버측에서 제공해준 랜덤 데이터를 가지고 premaster key를 생헝
      3. 생성된 premaster key를 public key로 암호화 후 서버측 전달(=> **비대칭 키 방식**)
   4. 서버측은 클라리언트 측이 제공한 암호화된 premaster key를 private key로 복호화하여 공통의 세션키(대칭키)를 획득
2. Transfer 1.주고받은 대칭키를 가지고 보낼 데이터가 있으면 암호화하여 보내고 받는 쪽은 복화화 수행(**대칭 키 방식**). 이를 통해 공격자로 부터 정보 노출 방어
3. Session Terminate
   1. 데이터 전송이 끝나면 SSL 통신이 끝났음을 서로에게 알린 후 생성된 대칭키 폐기

<img src="/public/img/SSL/handshake.png">

- **그림으로 보는 session key 생성 과정**
  <img src="/public/img/SSL/figure_keygen.png">

---

## Openssl을 활용한 인증서 발급 및 Nginx 적용

> 사설 인증서 발급 및 자체 서명

```bash
#public key 생성
openssl genrsa -out /etc/ssl/private/nginx-selfsigned.key 2048

#인증서 서명 요청(CSR, Certificate Signing Request) 생성
openssl req -new -key /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/nginx-selfsigned.csr


# 자체 서명된 인증서(CRT, Certificate) 발급
openssl x509 -req -days 365 -in /etc/ssl/nginx-selfsigned.csr -signkey /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/nginx-selfsigned.crt

```

> Nginx key/crt 적용 및 포트 설정

```
server {
    listen 443 ssl; # HTTPS 포트
    server_name your_domain.com;

    ssl_certificate /etc/ssl/nginx-selfsigned.crt;
    ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;

    access_log /root/access.log
    error_log /root/error.log

    # SSL 설정
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers on;
    ssl_ciphers 'ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256';

    location / {
        root /var/www/html;
        index index.html;
    }
}

# HTTP 요청을 HTTPS로 리다이렉트
server {
    listen 80;
    server_name your_domain.com;
    return 301 https://$server_name$request_uri;
}
```

---

## REF

- 생활코딩 : [link](https://opentutorials.org/course/228/4894)
- SSL Handshake : [link](https://babbab2.tistory.com/7)
- Key Generate : [link](https://mangkyu.tistory.com/98)
