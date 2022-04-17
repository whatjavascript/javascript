# 22장 this

### this

자신이 속한 객체를 가리키는 식별자

객체 리터럴 방식으로 생성한 객체의 경우 메서드 내부에서 메서드 자신이 속한 객체를 가리키는 식발자를 재귀적으로 참조

```jsx
const circle = {
	radius : 5,
	getDiameter(){
		return 2 * circle.radius;
	}
}
console.log(circle.getDiameter()); // 10
```

```jsx
function Circle(radius) {
	// 이 시점에는 생성자 함수 자신이 생성할 인스턴스를 가리키는 식별자를 알 수 없음
	????.radius = radius;
}
```

this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수. this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조 할 수 있음

this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 동적으로 결정

this는 코드 어디에서든 참조 가능, 전역에서도 함수 내부에서도 참조할 수 있음

### 함수 호출 방식과 this 바인딩

this 바인딩은 함수 호출 방식, 즉 함수가 어떻게 호출되었는지에 따라 동적으로 결정

1. 일반함수 호출
2. 메서드 호출
3. 생성자 함수 호출
4. Function.prototype.apply/call/bind 메서드에 의한 간접 호출

```jsx
// 1
const foo = function() {
	console.dir(this);
}

foo(); // window
// 2
const obj = { foo };
obj.foo(); // obj

// 3
new foo(); // foo {}

//4
const bar = { name: 'bar' };

foo.call(bar); // bar
foo.apply(bar); // bar
foo.bind(bar)(); // bar
```

일반 함수에서는 기본적으로 this에는 전역 객체 바인딩

중첩 함수도 마찬가지

```jsx
function foo() {
	console.log("foo's this: ", this); // window
	function bar() {
		console.log("bar's this: ", this); // window
	}
	bar();
}
foo();
```

strict mode가 적용된 일반 함수 내부에서는 this는 undefined

콜백 함수가 일반 함수로  호출된다면 콜백 함수 내부의 this에도 전역 객체가 바인딩 됨

```jsx
const obj = {
	value : 100,
	foo() {
		console.log('foo's this: ", this); // {value : 100, foo : f}
		// 콜백 함수 내부의 this에 전역 객체 바인딩
		setTimeout(function() {
			console.log("calback's this: ",  this); // window			
		}, 100);
	}
}
```

일반 함수로 호출된 모든 함수(중첩 함수, 콜백 함수 포함) 내부의 this에는 전역 객체 바인딩

this를 바인딩 시키는 방법

```jsx
const obj = {
	value: 100,
	foo() {
		// this 바인딩(obj)를 변수 that에 할당
		const that = this;
		// 콜백 함수 내부에서 this 대신 that 참조
		setTimeout(function(){
			console.log(that.value); // 100
		},100)
	}
};

const obj = {
	value: 100,
	foo() {
		// 콜백 함수에 명시적으로 this 바인딩
		setTimeout(function(){
			console.log(this.value); // 100
		}.bind(this),100);
	}
}

const obj = {
	value: 100,
	foo() {
		setTimeout(()=>console.log(this.value),100); //100
	}
}
```

**메서드 호출**

```jsx
const person {
	name: 'Lee',
	getName() {
		return this.name;
	}
}

console.log(person.getName()); // Lee
```

메서드는 프로퍼티에 바인딩된 함수

```jsx
const anotherPerson = {
	name: 'Kim'
};
// getName 메서드를 anotherPerson 객체의 메서드로 할당
anotherPerson.getName = person.getName;
// getName 메서드를 호출한 객체는 anotherPerson
console.log(anotherPerson.getName()); // Kim
// getName 메서드를 변수에 할당
const getName = person.getName;
// getName 메서드를 일반 함수로 호출
console.log(getName()); // ''
```

프로토타입 메서드 내부에서 사용된 this도 일반 메서드와 마찬가지로 해당 메서드를 호출한 객체에 바인딩

```jsx
function Person(name){
	this.name = name;
}
Person.prototype.getName = function() {
	return this.name;
}
```

**생성자 함수 호출**

생성자 함수 내부의 this에는 생성자 함수가 생설할 인스턴스 바인딩

```jsx
function Circle(radius){
	this.radius = radius;
	this.getDiameter = function() {
		return 2 * this.radius;
	};
}
```

**Function.prototype.apply/call/bind 메서드에 의한 간접 호출**

```jsx
function getThisBinding(){
	return this;
}

const thisArg = { a :1 };

console.log(getThisBinding()); // window

console.log(getThisBinding.apply(thisArg)); // {a: 1}
console.log(getThisBinding.call(thisArg)); // {a: 1}

console.log(getThisBinding.call(thisArg, [1,2,3])); // {a: 1}
console.log(getThisBinding.call(thisArg,1,2,3)); // {a: 1}
```

apply와 call 메서드의 본질적인 기능은 함수를 호출하는 것 첫 번째 인수로 전달한 특정 개체를 this에 바인딩

```jsx
const person = {
	name : 'Lee',
	foo(callback) {
		setTimeout(callback.bind(this),100);
	}
};

person.foo(function(){
	console.log(`Hi! my name is ${this.name}.`);
}
```