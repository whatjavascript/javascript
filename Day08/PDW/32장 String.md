# 32장 String

## String 생성자 함수

```jsx
const strObj = new String();
console.log(strObj); // String {length:0, [[PrimitiveValue]]: ""}
```

```jsx
const strObj = new String('Lee');
console.log(strObj);
//String {0: "L", 1:"e", 2:"e", length: 3, [[PrimitiveValue]]: "Lee"}

console.log(strObj[0]); // L
// 문자열은 원시 값이므로 변경할 수 없다. 에러는 발생하지 않는다.
strObj[0] = 'S';
console.log(strObj); // 'Lee'
```

String 생성자 함수의 인수로 문자열이 아닌 값을 전달하면 인수를 문자열로 강제 변환한 후 생성

## length 프로퍼티

length 프로퍼티는 문자열의 문자 개수를 반환

## String 메서드

문자열은 변경 불가능한 원시 값이기 때문에 **String 래퍼 객체도 읽기 전용 객체로 제공**

String 객체의 메서드는 언제나 새로운 문자열을 생성하여 반환

String.prototype.indexOf

```jsx
const str = 'Hello World';

str.indexOf('l'); // 2
str.indexOf('or'); // 7
str.indexOf('x'); // -1
str.indexOf('l',3); // 3
```

String.prototype.search

대상 문자열에서 인수로 전달받은 정규 표현식과 매치하는 문자열을 검색하여 일치하는 문자열 인덱스를 반환한다.

```jsx
const str = 'Hello World';

str.search(/o/); // 4
str.search(/x/); // -1
```

String.prototype.includes

```jsx
const str = 'Hello world';

str.includes('Hello'); // true
str.includes(' '); // true
str.includes('x'); // false
str.includes(); // false

str.includes('l',3) // true
```

String.prototype.startsWith

```jsx
const str = 'Hello world';
str.startsWith('He'); // true
str.startsWith('x'); // false

str.startsWith(' ', 5); // true;
```

String.prototype.endsWith

```jsx
const str = 'Hello world';

str.endsWith('ld'); // true
str.endsWith('x'); // false

str.endsWith('lo', 5); // true
```

String.prototype.charAt

charAt 메서드는 대상 문자열에서 인수로 전달받은 인덱스에 위치한 문자를 검색하여 반환한다.

String.prototype.substring

```jsx
const str = 'Hello World';
// 인덱스 1부터 인덱스 4 이전까지의 부분 문자열 반환
str.substring(1,4); // ell

str.substring(1); // 'ello World'
```

String.prototype.slice

substring과 동일하게 동작한다. 대신 음수인 인수를 전달 할 수 있다. 음수인 인수를 전달하면 대상 문자열의 가장 뒤에서부터 시작하여 문자열을 잘라 반환한다.

```jsx
const str = 'hello world';

str.substring(0,5);
str.slice(0,5);

str.substring(-5); // 'hello world'
str.slice(-5); // world
```

String.prototype.toUpperCase

대상 문자열을 모두 대문자로 변경한 문자열을 반환한다.

String.prototype.toLowerCase

대상 문자열을 모두 소문자로 변경한 문자열을 반환한다.

String.prototype.trim

대상 문자열 앞뒤에 공백 문자가 있을 경우 이를 제거한 문자열을 반환한다.

String.prototype.repeat

대상 문자열을 인수로 전달받은 정수만큼 반복해 연결한 새로운 문자열을 반환

0이면 빈 문자열을 반환하고 음수면 RangeError를 발생, 인수 생략 시 0으로 설전된다.

String.prototype.replace

대상 문자열에서 첫 번째 인수로 전달받은 문자열 또는 정규 표현식을 검색하여 두번 째 인수로 전달한 문자열로 치환한 문자열을 반환한다.

```jsx
const str = 'Hellow world';

str.replace('world', 'Lee'); 
```

replace 메서드의 두번 째 인수로 치환 함수를 전달 할 수 있다.

```jsx
function camelToSnake(camelCase){
	return camelCase.replace(/.[A-Z]/g, match => {
		return match[0] + '_' + match[1].toLowerCase();
	});
}

function snakeToCamel(snakeCase){
	return snakeCase.replace(/_[a-z]/g, match=> {
		return match[1].toUpperCase();
	}
}
```

String.prototype.split

대상 문자열에서 첫 번째 인사로 전달한 문자열 또는 정규 표현식을 검색하여 문자열을 구분한 후 분리된 각 문자열로 이루어진 배열을 반환

두 번째 인수로 배열의 길이를 지정할 수 있다.

```jsx
const str = 'How are you doing';
str.split(' ', 3); // ["How", "are", "you"]
```