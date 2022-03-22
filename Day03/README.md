# 2022-03-22 스터디 리뷰

## 9장 타입 변환과 단축 평가
    
    논리곱 연산자는 좌항에서 우항으로 평가가 진행됨 → 논리 연산의 결과를 결정하는 두번째 피연산자를 그대로 반환한다.

    옵셔널 체이닝 연산자

    옵셔널 체이닝 연산자 ?. 는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.
```
    var elem = null;

    var value = elem?.value;
    console.log(value); // undefined

    // 단축평과와 다른 필요성
    var str = '';
    var length = str && str.length; // ''

    var str = '';
    var length = str?.length; // 0
```



## 11장 원시 값과 객체의 비교
    원시값의 불변성
    불변성을 갖는 원시 값을 할당한 변수는 재할당 이외에 변수 값을 변경할 수 있는 방법이 없음

## 12장 함수
    호이스팅function hoisting이란 함수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징이다

## 13장 스코프
    1. 함수를 어디서 호출했는지에 따라 함수의 상위 스코프를 결정한다. → 동적 스코프
    2. 함수를 어디서 정의했는지에 따라 함수의 상위 스코프를 결정한다. → 렉시컬/정적 스코프
## 14장 전역 변수의 문제점
    호이스팅은 스코프 단위

## 15장 let, const 키워드와 블록 레벨 스코프
    let , const, class 호이스팅은 하지만 안하는 것 처럼 보임


## 16장 프로퍼티 어트리뷰트
### 프로퍼티 어트리뷰트 접근하는 이유
    - 객체 안에 메서드를 확인 할 수 있음
    - 추측으로는 속성이나 메서드의 내용과 속성을 확인할 수 있음

## 17장 생성자와 함수에 의한 객체 생성
    constructor와 non-constructor의 구분

    constructor : 함수 선언문, 함수 표현식, 클래스

    not-constructor : 메서드(ES6 메서드 축약 표현) , 화살표 함수

##  18장 함수와 일급객체
    가변인자 argumets 객체 사용 

    참고 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments