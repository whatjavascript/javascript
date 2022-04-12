# 19장 프로토타입

### 프로토타입 객체
- 프로토타입 객체란 객체지향 프로그래밍의 근간을 이루는 객체 간 상속을 구현하기 위해 사용된다

### __proto__를 접근하는 이유
- 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위해서
```
const parent = {};
const child = {};

// child의 프로토타입을 parent로 설정
child.__proto__ = parent;
// parent의 프로토타입을 child로 설정
parent.__proto__ = child; // TypeError: Cyclic __proto__ value
```

### 프로토 타입 생성 시점
- 생성자 함수가 생성되는 시점에 생성되며 non-constructor는 프로토타입이 생성되지 않음
