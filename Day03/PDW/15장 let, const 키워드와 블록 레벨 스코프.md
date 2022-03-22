# 15 let, const 키워드와 블록 레벨 스코프

### var 키워드로 선언한 변수의 문제점

1. **var 키워드로 선언한 변수는 중복 선언 가능**
2. **함수 레벨 스코프** 
    
    var 키워드로 선언한 변수는 오로지 함수의 코드 블록만을 지역 스코프로 인정
    
    ```jsx
    var x = 1;
    if(true) {
    	var x= 10;
    }
    console.log(x); // 10
    
    var i = 10;
    for (var i= 0; i<5; i++){
    	console.log(i); 
    }
    // 의도치 않게 i 변수의 값이 변경
    console.log(i); // 5
    ```
    
3. **변수 호이스팅**
    
    변수 호이스팅에 의해 var 키워드로 선언한 변수는 변수 선언문 이전에 참조할 수 있어 에러를 발생시키지 않지만 프로그램 흐름상도 맞지 않고 가독성을 떨어뜨리며 오류를 발생시킬 여지를 남김
    

### let 키워드

var 키워드의 단점을 보완하기 위해 ES6에서는 새로운 변수 선언 키워드인 let, const를 도입

1. **변수 중복 선언 금지**
2. **블록 레벨 스코프**

```jsx
let foo =1;
{
	let foo = 2;
	let bar = 3;
}
console.log(foo) // 1
console.log(bar) // 3
```

1. **변수 호이스팅**

var 키워드로 선언한 변수와 달리 let 키워드로 선언한 변수는 변수 호이스팅이 발생하지 않는 것처럼 동작

**let 키워드로 선언한 변수는 선언 단계와 초기화 단계가 분리되어 진행**

스코프의 시작 지점부터 초기화 시작 시점까지 변수를 참조할 수 없는 구간을 **일시적 사각지대**라고 함 → let 키워드

```jsx
console.log(foo); // ReferenceError : foo is not defined

let foo; // 변수 선언문에서 초기화 단계 실행
console.log(foo); // undefined

foo = 1;
console.log(foo); // 1
```

자바스크립트 ES6 에 도입된 let, const를 포함해서 모든 선언(let, const,function,function*, class)은 호이스팅함.

let, const, class 를 사용한 선언문은 호이스팅이 발생하지 않는 것처럼 동작

1. **전역 객체와 let**

var 키워드로 선언한 전역 변수와 전역 함수, 그리고 선언하지 않은 변수에 값을 할당한 암묵적 전역은 전역 객체 window의 프로퍼티가 됨

let 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다.

### const 키워드

상수 선언을 위해 사용

1. **선언과 초기화**
    
    **const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화**
    
    let 와 같은 블록스코프, 변수 호이스팅이 발생하지 않는 것처럼 동작
    
2. **재할당 금지**
3. **상수**
    
    **상수는 재할당이 금지된 변수**
    
4. **const 키워드와 객체**
    
    **const 키워드로 선언된 변수에 객체를 할당한 경우 값을 변경할 수 있음**
    
    ```jsx
    const person = {
    	name : 'Lee'
    };
    
    person.name = 'Kim';
    
    console.log(person);
    ```
    
    객체는 재할당 없이도 직접 변경이 가능하기 때문 → **const 키워드는 재할당을 금지할 뿐 “불변”을 의미하지 않음**
    

### var vs let vs const

변수 선언에는 기본적으로 const , 재할당이 필요한 경우에 한정해 let를 사용하는 것이 좋음

ES6를 사용한다면 var 키워드 사용하지 않는다.

변수 선언할 때는 일단 const 키워드를 사용