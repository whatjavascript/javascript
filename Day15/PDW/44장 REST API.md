# 44장 REST API

### REST API의 구성

REST API는 자원, 행위, 표현 3가지 요소로 구성된다. REST는 자체 표현구조로 구성되어 REST API 만으로 HTTP 요청의 내용을 이해할 수 있다.

자원 : URL

행위 : HTTP 요청 메서드

표현 : 페이로드

### REST API 설계 원칙

**URL은 리소스 표현**에 집중하고 **행위에 대한 정의는 HTTP 요청 메서드를 통해 하는 것**이 RESTful API를 설계하는 중심 규칙