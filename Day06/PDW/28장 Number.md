# 28장 Number

### Number 생성자 함수

```jsx
const numObj = new Number();
console.log(numObj); // Number {[[PrimitiveValue]] : 0}
```

### Number 프로퍼티

**Number.EPSILON**

EPSILON은 1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이

```jsx
0.1 + 0.2 === 0.3 // false
function isEqual(a,b) {
	return Math.abs(a-b) < Number.EPSILON;
}
isEqual(0.1 + 0.2, 0.3); // true
```

**Number.MAX_VALUE**

자바스크립트에서 표현할 수 있는 가장 큰 양수 값

**Number.MIN_VALUE**

자바스크립트에서 표현할 수 있는 가장 작은 양수 값

**Number.MAX_SAFE_INTEGER**

자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수 값

**Number.MIN_SAFE_INTEGER**

자바스크립트에서 안전하게 표현할 수 있는 가장 작은 정수 값

**Number.POSITIVE_INFINITY**

양의 무한대를 나타내는 숫자값 Infinity와 같음

**Number.NEGATIVE_INFINITY**

음의 무한대를 나타내는 숫자값 -Infinity와 같음

**Number.NaN**

window.Nan 과 같음

### Number 메서드

[Number.is](http://Number.is)Finite

인수로 전달된 숫자값이 정상적인 유한수인지 검사하여 불리언 값 반환

숫자가 아닌 수가 주어지면 반환 값은 false

```jsx
Number.isFinite(null); // false
isFinite(null); // true
```

**Number.isInteger**

정수 인지 검사하여 그 결과 불리언 값으로 반환

**Number.isNaN** 

NaN인지 검사하여 그 결과를 불리언 값으로 반환

```jsx
Number.isNaN(undefined); // false
isNaN(undefined); // true
```

**Number.isSafeInteger**

안전한 정수인지 검사하여 불리언 값으로 반환

**Number.prototype.toExponential**

```jsx
(77.1234).toExponential(); // -> "7.71234e+1"
(77.1234).toExponential(4); // -> "7.7123e+1"
(77.1234).toExponential(2); // -> "7.71e+1"
```

**Number.prototype.toFixed**

```jsx
(12345.6789).toFixed(); // 12346 소수점이하 반올림
(12345.6789).toFixed(1); // 12345.7 소수점이하 반올림
```

**Number.prototype.toPrecision**

```jsx
(12345.6789).toPrecision(); //  "12345.6789"
(12345.6789).toPrecision(1); //  "1e+4"
```

**Number.prototype.toString**

```jsx
(10).toString(); // 10
(16).toString(2); // 10000
(10).toString(8); // 20
(10).toString(16); // 10

```