# 43장 Ajax

### Ajax란?

AJax란 자바스크립트를 사용하여 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, 서버가 응답한 데이터를 수신하여 웹페이지를 동적으로 갱신하는 프로그래밍 방식을 말함

Ajax는 브라우저에서 제공하는 Web API인 XMLHttpRequest 객체를 기반으로 동작, XMLHttpRequest는 HTTP 비동기 통신을 위한 메서드와 프로퍼티를 제공함

### JSON

JSON은 클라이언트와 서버 간의 HTTP 통신을 위한 텍스트 데이터 포맷이다. 자바스크립트에 종속되지 않는 언어 독립형 데이터 포맷으로 대부분의 프로그래밍에서 사용 가능하다.

JSON.stringify

객체를 JSON 포맷의 문자열로 변환한다. 

JSON.parse

JSON 포맷의 문자열을 객체로 변환

### XMLHttpRequest

Web API인 XMLHttpRequest 객체는 HTTP 요청 전송과 HTTP 응답 수신을 위한 다양한 메서드와 프로퍼티를 제공함

객체 생성

```jsx
const xhr = new XHMLHttpRequest();
```

프로퍼티와 메서드

readyState 

- HTTP 요청의 현재 상태를 나타내는 정수, 다음과 같은 XMLHttpRequest 정적 프로퍼티를 값으로 갖는다.
    - UNSENT : 0
    - OPENED : 1
    - HEADERS_RECEIVED : 2
    - LOADING : 3
    - DONE : 4

status

- HTTP 요청에 응답 상태를 나타내는 정수

statusText 

- HTTP 요청에 대한 응답 메시지를 나타내는 문자열

responseType

- HTTP 응답 타입

resopnse

- HTTP 요청에 대한 응답 몸체, responseType에 따라 타입이 다르다.

responseText

- 서버가 전송한 HTTP 요청에 대한 응답 문자열

**HTTP 요청 전송**

1. [XMLHttpReqeust.prototype.open](http://XMLHttpReqeust.prototype.open) 메서드로 HTTP 요청을 초기화 한다.
2. 필요에 따라 XMLHttpRequest.prototype.setRequestHeader 메서드로 특정 HTTP 요청의 헤더 값을 설정
3. XMLHttpRequest.prototype.send 메서드를 HTTP 요청을 전송

**XMLHttpRequest.prototype.open**

```jsx
xhr.open(method,url[,async])
```

주로 사용되는 5가지 메서드

- GET : 모든 /특정 리소스 취득
- POST : 리소스 생성
- PUT: 리소스 전체 교체
- PATCH: 리소스 일부 수정
- DELETE: 모든/특정리소스 삭제

**XMLHttpRequest.prototype.send**

open 메서드로 초기화된 HTTP 요청을 서버에 전송, 기본적으로 서버로 전송하는 데이터는 GET, POST 요청 메서드에 따라 전송 방식에 차이가 있음

```jsx
xhr.send(JSON.stringify({id : 1, content: 'HTML', completed: false}));
```

HTTP 요청 메서드가 GET 인 경우 send 메서드에 페이로드로 전달한 인수는 무시되고 요청 몸체는 null로 설정된다.

**XMLHttpRequest.prototype.setRequestHeader**

setRequestHeader 메서드는 특정 HTTP 요청의 헤더 값을 설정

```jsx
const xhr = new XMLHttpRequest();

xhr.opne('POST', '/users');

xhr.setRequestHeader('content-type' , 'application/json');

xhr.send(JSON.stringify({id : 1, content: 'HTML', completed: false}));
```

**HTTP 응답 처리**

```jsx
const xhr = new XMLHttpRequest();

xhr.open('GET', 'https://jsonplaceholder.typicode.com/todos/1');

xhr.send();

// readyState 프로퍼티가 변경될 때마다 발생
xhr.onreadystatechange = () => {
	if(xhr.readyState !== XMLHttpRequest.DONE) return;

	if(xhr.status === 200) {
		console.log(JSON.parse(xhr.response));
	} else {
		console.error('Error', xhr.status, xhr.statusText);
	}
}
```