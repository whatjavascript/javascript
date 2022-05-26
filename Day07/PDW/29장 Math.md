# 29장 Math

### Math

프로퍼티

Math.PI

```jsx
Math.PI; // 3.1415922653589793
```

메서드

Math.abs

```jsx
Math.abs(-1) // 1
Math.abs('-1') // 1
Math.abs('') // 0
Math.abs([]) // 0
Math.abs(null) // 0
Math.abs(undefined) // NaN
Math.abs({}) // NaN
Math.abs('string'); // NaN
Math.abs() // NaN
```

Math.round

인수로 전달된 숫자의 소수점 이하를 반올림한 정수를 반환

Math.ceil

인수로 전달된 숫자의 소수점 이하를 올림한 정수를 반환

Math.floor

인수로 전달된 숫자의 소수점 이하를 내림한 정수를 반환

Math.sqrt

인수로 전달된 숫자의 제곱근을 반환

Math.random

임의의 난수(0이상~1 미만의 실수)를 반환

Math.pow

첫 번째 인수를 밑으로 두 번째 인수를 지수로 거듭제곱한 결과 반환

→ 지수 연산자 **를 사용하면 가독성이 더 좋음

Math.max

전달 받은 인수 중에서 가장 큰 수를 반환

Math.min

전달 받은 인수 중에서 가장 작은 수를 반환