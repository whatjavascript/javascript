# 46장 제네레이터와 async/await

### 제네레이터란?

제네레이터는 코드 블록의 실행을 일시 중지했다가 필요한 시점에 재개할 수 있는 특수한 함수이다.

- 제네레이터 함수는 함수 호출자에게 함수 실행의 제어권을 양도할 수 있다.
- 제네레이터 함수는 함수 호출자와 함수의 상태를 주고받을 수 있다.
- 제네레이터 함수를 호출하며 제네레이터 객체를 반환한다.

### 제네레이터 함수의 정의

```jsx
// 제네레이터 함수 선언문
function* genDecFunc() {
	yield 1;
}

// 제네레이터 함수 표현식
const genExpFunc = function* () {
	yield 1;
}

// 제네레이터 메서드
const obj = {
	* genObjMethod(){
		yield 1;
	}
};
// 제네레이터 클래스 메서드
class MyClass {
	* genClsMethod() {
		yield 1;
	}
}
```

화살표 함수로 정의 할 수 없다.

### 제네레이터 객체

제네레이터 함수를 호출하면 일반 함수처럼 함수 코드 블록을 실행하는 것이 아니라 제네레이터 객체를 생성해 반환한다. 제네레이터 함수가 반환 제네레이터 객체는 이터러블이면서 동시에 이터레이터다.

```jsx
function* genFunc() {
	yield 1;
	yield 2;
	yield 3;
}

const generator = genFunc();

console.log(Symbol.iterator in generator); //true;
console.log('next' in generator); // true
```

```jsx
function* genFunc() {
	try {
		yield 1;
		yield 2;
		yield 3;
	} catch (e) {
		console.error(e)
	}
}
const generator = genFunc();
console.log(generator.next()); // {value: 1, done: false}
console.log(generator.return('End!')); // {value: "End!", done: true}
```

### 제네레이터의 일시 중지와 재개

yield 키워드는 제네레이터 함수의 실행을 일시 중지시키거나 yield 키워드 뒤에 오는 표현식의 평가 결과를 제네레이터 함수 호출자에 반환한다.

```jsx
function* genFunc() {
	yield 1;
	yield 2;
	yield 3;
}

const generator = genFunc();
console.log(generator.next()); // {value: 1, done: false}

console.log(generator.next()); // {value: 2, done: false}
console.log(generator.next()); // {value: 3, done: false}
console.log(generator.next()); // {value: undefined, done: true}

```

제네레이터 객체의 next 메서드를 호출하면 yield 표현식까지 실행되고 일시 중지된다. 이때 함수의 제어권이 호출자로 양도된다.

제네레이터 객체의 next 메서드는 value, done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환한다.

제네레이터 객체의 next 메서드에 전달한 인수는 제네레이터 함수의 yield 표현식을 할당받는 변수에 할당된다.

```jsx
function* genFunc() {
	const x = yield 1;
	const y = yield (x+10);
	return x +  y;
}

const generator = genFunc(0);
let res = generator.next(); // {value: 1, done: false}
res = generator.next(10); // {value: 20, done: false}
res = generator.next(20); // {value: 30, done: false}
```

### 제네레이터의 활용

```jsx
const infiniteFibonacci  = (function () {
	let [pre, cur] = [0, 1];
	return {
		[Symbol.iterator]() { return this; },
		next() {
			[pre, cur] = [cur, pre + cur];
			return { value: cur };
		}
	};
}());

for(const num of infiniteFibonacci) {
	if(num > 10000) break;
	console.log(num);
}

const infiniteFibonacci  = (function () {
	let [pre, cur] = [0, 1];
	
	while(true) {
		[pre, cur] = [cur, pre + cur];
		yield cur;
	}
}());
```

### async/await

제네레이터보다 간단하고 가독성 좋게 비동기 처리를 동기 처리처럼 동작하도록 구현할 수 있는 async/await 가 도입

**async 함수**

await 키워드는 반드시 async 함수 내부에서 사용해야함, async 함수는 async 키워드를 사용해 정의하며 언제나 프로미스를 반환. async 함수가 명시적으로 프로미스를 반환하지 않더라도 async 함수는 암묵적으로 반환값을 resolve하는 프로미스를 반환한다.

```jsx
async function foo(n) {return n;}
foo(1).then(v => console.log(v));
```

**await 키워드**

await 키워드는 프로미스가 settled 상태가 될 때 까지 대기하다가 settled 상태가 되면 프로미스가 resolve한 처리 결과를 반환한다.

```jsx
const fetch = require('node-fetch');

const getGithubUserName = async id => {
	const res = await fetch(`https://api.github.com/users/${id}`);
	const {name} = await res.json();
	console.log(name);
}
getGithubUserName('ungmo2');
```

**에러처리**

async 함수 내에서 catch 문을 사용해서 에러 처리를 하지 않으면 async 함수는 발생한 에러를 reject 하는 프라미스를 반환한다