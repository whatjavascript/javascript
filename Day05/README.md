# 5주차 리뷰

## 22장 this
- this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수다. this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.
- 함수호출과 this 바인딩

    | 함수 호출 방식 | this 바인딩 |
    | --- | --- |
    | 일반 함수 호출 | 전역 객체 |
    | 메서드 호출 | 메서드를 호출한 객체 |
    | 생성자 함수 호출 | 생성자 함수가 (미래에) 생성할 인스턴스 |
    | Function.prototype.apply/call/bind 메서드에 의한 간접 호출 | Function.prototype.apply/call/bind 메서드에 첫번째 인수로 전달한 객체 |


## 23장 실행 컨텍스트 🔥🔥 

- 자바스크립트의 코드들이 실행되기 위한 환경

- 전역 컨텍스트, 함수 컨텍스트 2가지 존재

- 전역 컨텍스트 하나 생성 후에 함수 호출할 때마다 함수 컨텍스트가 생성

- 컨텍스트를 생성시에 변수객체, 스코프 체인, this가 생성된다.

- 컨텍스트 생성 후 함수가 실행되는데 사용되는 변수들은 변수 객체 안에서 값을 찾고 없다면 스코프체인을 따라 올라가며 찾음.

- 함수 실행이 마무리되면 해당 컨텍스트는 사라짐. 페이지가 종료되면 전역 컨텍스트가 사라짐

- 즉, 자바스크립트의 코드가 실행되기 위해서는 변수객체, 스코프체인, this 정보들을 담고 있는 곳을 실행 컨텍스트라고 부른다.

## 24장 클로저

- 반환된 내부함수가 자신이 선언됬을때의 환경인 스코프를 기억하여 자신이 선언되었을때의 환경 밖에서 호출되어도 그 환경에 접근할 수 있는 함수, 자신이 생성될때의 환경을 기억하는 함수 

- 사용 이유
    1) 현재 상태를 기억하고 변경된 최신 상태를 유지하기 위해
    2) 전역 변수의 사용을 억제 하기 위해
    3) 정보를 은닉하고 특정 함수에게만 상태를 변경을 허용하기 위해
    4) 실수를 줄이기 위해

## 25장 클래스
- 함수와 달리 호이스팅이 발생하지 않는 것 처럼 동작하며 일급 객체

- 일급객체 특징
    - 무명의 리터럴로 생성할 수 있음
    - 변수나 자료구조에 저장할 수 있음
    - 함수의 매개변수에 전달 가능
    - 함수의 반환값으로 사용

## 26장 ES6
 - ES6 에서 추가된 스펙
    - let, const, 화살표함수, rest 파라미터, 클래스, 프로미스, 스프레드 연산자 등