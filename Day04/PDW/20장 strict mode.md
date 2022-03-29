# 20장 strict mode

### strict mode란?

strict mode는 자바스크립트 언어의 문법을 좀 더 엄격히 적용하여 오류를 발생시킬 가능성이 높거나 자바스크립트 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 명시적 에러 발생

### **strict mode의 적용**

strict mode를 적용하려면 전역의 선두 또는 함수 몸체의 선두에 ‘use strict’; 추가

### 전역에 strict mode 적용하는 것은 피하자

전역에 적용한 strict mode는 스크립트 단위로 적용

```jsx
<script>
	'use strict';
</script>
<script>
	x = 1; // 에러가 발생하지 않는다.
</script>

```

strict mode 스크립트와 non-strict mode 스크립트를 혼용하는 것은 오류를 발생시킬 수 있다. 즉시 실행 함수로 스크립트를 전체를 감싸서 스코프를 구분하고 즉시 실행 함수의 선두에 strict mode를 적용

```jsx
(function(){
	'use strict';
}());
```

### 함수 단위로 strict mode를 적용하는 것도 피하자

strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직함

### strict mode 가 발생시키는 에러

**암묵적 전역**

```jsx
(function(){
	'use strict';
	x = 1;
	console.log(x); // ReferenceError: x is not defined
}());
```

**변수, 함수, 매개변수의 삭제**

```jsx
(function() {
	'use strict'
	var x = 1;
	delete x; // SyntaxError: Delete of an unqualified identifier in strict mode.
	function foo(a){
		delete a; // SyntaxError: Delete of an unqualified identifier in strict mode.
	}
	delete foo; // SyntaxError: Delete of an unqualified identifier in strict mode.
}());
```

**매개변수 이름의 중복**

```jsx
(function() {
	'use strict';
	
	//SyntaxError: Duplicate parameter name not allowed in this context
	function foo(x,y){
		return x +x;
	}
	console.log(foo(1,2));
}());
```

**with문의 사용**

with문은 동일한 객체의 프로퍼티를 반복해서 사용할 때 객체 이름을 생략할 수 있어서 코드가 간단해지는 효과가 있지만 성능과 가독성이 나빠지는 문제가 있음, 사용하지 않는 것이 좋음

### strict mode 적용에 의한 변화

**일반 함수의 this**

strict mode 에서 함수를 일반 함수로서 호출하면 this에 undefined가 바인딩된다. 생성자 함수가 아닌 일반 함수 내에서는 this를 사용할 필요가 없기 떄문이다. 에러는 발생하지 않는다.

```jsx
(function() {
	'use strict';
	function foo(){
		console.log(this); // undefined
	}
	foo();
	
	function Foo(){
		console.log(this); // Foo
	}
	new Foo();
}());
```

**arguments 객체**

strict mode에서는 매개변수에 전달된 인수를 재할당하여 변경해도 arguments객체 에 반영되지 않음

```jsx
(function (a) {
	'use  strict';
	// 매개변수에 전달된 인수를 재할당하여 변경
	a = 2;
	// 변경된 인수가 arguments 객체에 반영되지 않음
	console.log(arguments); // { 0 : 1, length: 1 }
}(1));
```