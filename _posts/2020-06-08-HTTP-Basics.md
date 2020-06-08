---
title: "HTTP Basics"
categories: 
  - dev
last_modified_at: 2020-06-08T00:00:00+09:00
toc: true
author_profile: true
tag: 
  - http
---

# HTTP 기초

웹 개발의 기초가 되는 HTTP에 대한 내용을 간략히 정리해보았다.

## HTTP 통신 (Hyper Text Transfer Protocol)

> *Hyper Text*란?
> HTML(Hyper Text Markup Language)로 표현되는 웹 문서

### HTTP 통신 과정

1. TCP 연결을 염
2. HTTP 메시지를 전송 (Request)
3. 서버에 의해 전송된 응답을 읽음 (Response)
4. 연결을 닫거나 연결을 재사용

## HTTP Request

* Method: HTTP Method. GET이나 POST, OPTIONS, HEAD..
* Path: Resource의 경로
* Version of the protocol
* Headers
* Body: 평문

## HTTP Response

* Version of the protocol
* Status code: 요청의 성공 여부 / 이유
* Status message: Status code에 대한 짧은 설명
* Headers
* Body: 평문


## HTTPS (HyperText Transfer Protocol Secure)

> SSL(Secure Socket Layer)를 사용한 HTTP 프로토콜

SSL을 사용하기 위해서는 SSL인증서가 필요하다. (SSL 인증서에는 SSL 통신에 사용할 공개키가 들어있다.)

1. Client - Server Handshake중 client가 생성한 랜덤 데이터와 server가 생성한 랜덤 데이터로 대칭키를 생성
2. Cilent는 대칭키로 데이터를 암호화 후 공개키로 대칭키를 암호화
3. 암호화한 데이터와 대칭키를 Server에 전송
4. Server는 비밀키로 암호화된 대칭키를 복호화 후 복호화 된 대칭키로 암호화된 데이터를 복호화

## HTTP Method

* GET: 특정 리소스의 데이터를 받음
* POST: 특정 리소스에 엔티티를 제출
* PUT: 목적 리소스의 전체 내용을 Request Payload로 변경
* DELETE: 특정 리소스를 삭제
* HEAD: GET과 비슷하지만 Response Body를 포함하지 않음
* CONNECT: 서버와 양방향 연결을 시작. SSL연결을 시작할 때 사용 가능
* OPTIONS: 목적 리소스와의 통신 옵션을 설정
* TRACE: 목적 리소스의 경로를 따라 메시지 loopback 테스트 (Request내용이 그대로 돌아옴) - XST공격에 취약 (쿠키 등)
* PATCH: 목적 리소스의 내용을 부분적으로 변경

## HTTP Response Code

* 100 - 199: 정보성 코드
	* 101: Switching Protocols - 서버에 프로토콜 전환을 요청, 서버에서 승인 중
* 200 - 299: 성공 코드
	* 200: OK - Request가 정상이며 Body에 요청한 리소스가 있다.
	* 201: Created - 생성 Request를 성공하였다.
	* 204: No Content - Request는 정상이지만 제공할 내용이 없다.
* 300 - 399: 리다이렉션 코드
	* 301: Moved Permanently - 요청한 URL이 옮겨짐
* 400 - 499: 클라이언트 에러 코드
	* 400: Bad Request - Request가 잘못됨
	* 401: Unauthorized - 권한이 필요함
	* 403: Forbidden - 서버가 Request를 거부함
	* 404: Not Found - 요청한 URL을 찾을 수 없음
* 500 - 599: 서버 에러 코드
	* 500: Internal Server Error - 서버에 오류가 발생
	* 501: Not Implemented - Request에 대한 Response 기능이 없음
	* 502: Bad Gateway - Proxy나 Gateway서버에서 보냄. 
	* 503: Service Unavailable - 현재 유지보수 등으로 서버가 사용 불가
	* 504: Gateway Timeout - 응답 지연 발생으로 처리 불가


## Cookie & Session

> HTTP의 특징: Connectionless & Stateless
> Server에 Request를 보내고 필요한 파일을 받고나면 접속이 종료됨.

Server에서는 Client가 접속하고 있는 지 알 수 없다.
그래서 Cookie나 Session을 사용한다.

### Cookie

* Client 로컬에 저장되는 키와 값이 들어있는 데이터 파일
* 이름, 값, 만료날짜, 경로 
* 로컬에 최대 300개 저장 가능, 하나의 도메인당 최대 20개, 한 쿠키는 최대 4KB
* ex) 자동로그인, 장바구니 등

### Session

* 일정시간 같은 브라우저의 상태를 브라우저를 종료할 때 까지 유지
* Client가 Server에 접속 시 Server는 세션 ID를 발급
* 발급된 세션 ID는 쿠키로 저장
* 세션은 Server에 저장되는 정보
* ex) 로그인 유지

### References
* https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP
* https://opentutorials.org/course/228/4894
