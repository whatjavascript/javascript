# 33장 데이터 타입 Symbol

## 심벌이란?

- ES6에서 도입된 7번째 데이터 타입으로 변경 불가능한 원시 타입의 값

## 심벌 값의 생성

### Symbol 함수

- 다른 값과 절대 중복되지 않는 유일무이한 값

```jsx
const mySymbol = Symbol();
console.log(typeof mySymbol); // symbol

console.log(mySymbol);// Symbol()
```

- new 연산자와 함께 호출하지 않는다

```jsx
const mySymbol1 = Symbol('mySymbol');
const mySymbol2 = Symbol('mySymbol');

console.log(mySymbo1 === mySymbol2); // false
```

```jsx
const mySymbol = Symbol('mySymbol');

console.log(mySymbol.description); // mySymbol
console.log(mySymbol.toString()); // Symbol(mySymbol)
```

### Symbol.for / Symbol.keyFor 메서드

인수로 전달받은 문자열을 키로 사용하여 키와 심벌 값의 쌍들이 저장되어 있는 전역 심벌 레지스트리에서 해당 키와 일치하는 심벌 값 검색

```jsx
const s1 = Symbol.for('mySymbol');

const s2 = Symbol.for('mySymbol');

console.log(s1 === s2); // true
```

Symbol.keyFor 메서드를 사용하면 전역 심벌 레지스트리에 저장된 심벌 값의 키를 추출

```jsx
const s1 = Symbol.for('mySymbol');

Symbol.keyFor(s1); // mySymbol

const s2 = Symbol('foo');

Symbol.keyFor(s2); // undefined
```

## 심벌과 상수

- 특별한 의미가 없고 상수 이름 자체에 의미가 있는 경우 심볼을 사용

## 심벌과 프로퍼티 키

- 객체의 프로퍼티 키는 빈 문자열을 포함하는 모든 문자열 또는 심벌 값으로 만들 수 있으며 동적 생성 가능
- 심벌 값으로 프로퍼티 키를 동적 생성하여 프로퍼티를 만드려면 프로퍼티 키로 사용할 심벌 값에 대괄호를 사용

```jsx
const obj = {
	[Symbol.for('mySymbol')]: 1
}

obj[Symbol.for('mySymbol')]; // 1
```

심벌 값은 유일무이한 값이므로 심벌 값으로 프로퍼티 키를 만들면 다른 프로퍼티키와 절대 충돌하지 않는다.

## 심벌과 프로퍼티 은닉

```jsx
const obj = {
	[Symbol('mySymbol')]: 1
};

for (const key in obj) {
	console.log(key);
}

console.log(Object.key(obj)); // []
console.log(Object.getOwnPropertyNames(obj)); // []
```

```jsx
const obj = {
	[Symbol('mySymbol')]: 1
};

console.log(Object.getOwnPropertySymbols(obj)); // [Symbol(mySymbol)]

const symbolKey1 = Object.getOwnPropertySymbols(obj)[0];
console.log(obj[SymbolKey1]);
```

## 심벌과 표준 빌트인 객체 확장

```jsx
// 표준 빌트인 객체를 확장하는 것은 권장하지 않는다.
Array.prototype.sum = function() {
	return this.reduce((acc,cur)=> acc+cur, 0);
}

[1, 2].sum(); // 3

// 심벌 값으로 프로퍼티 키를 동적 생성하면 다른 프로퍼티 키와 절대 충돌하지 않아 안전하다.
Array.prototype[Symbol.for('sum')] = function () {
	return this.reduce((acc,cur) => acc + cur, 0);
}

[1, 2][Symbol.for('sum')](); // 3
```

## Well-known Sybol

자바스크립트가 기본 제공하는 빌트인 심벌 값을 ECMAScript 사양에서는 Well-known Symbol이라 함

```jsx
const iterable = {
	[Symbol.iterator](){
		let cur =1;
		const max = 5;
		return {
			next() {
				return { value: cur++ , done: cur > max +1 }
			}
		}
	}
}

for (const num of iterable) {
	console.log(num); // 1 2 3 4 5
}
```