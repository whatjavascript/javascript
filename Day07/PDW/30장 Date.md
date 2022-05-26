# 30장 Date

현재 날짜와 시간은 자바스크립트 코드가 실행된 시스템의 시계에 의해 결정

### Date 생성자 함수

- Date는 생성자 함수
- 1970년 1월 1일 00:00:00(UTC)를 기점으로 Date 객체가 나타내는 날짜와 시간까지의 밀리초를 나타냄
- 1970년 1월 2일 0시를 나타내면 내부적으로 24h * 60m *60s * 1000ms 인 86400000

### Date 객체 생성

1. new Date()

```jsx
new Date();
```

1. new Date(miliseconds)
- 1970년 1월 1일 00:00:00을 기점으로 인수로 전달된 밀리초만큼 경과한 날짜와 시간을 나타내는 Date 객체 반환

```jsx
// 한국 표준시 KST는 협정 세계시 UTC에 9시간을 더한 시간
new Date(0); // Thu Jan 01 1970 09:00:00 GMT+0900 (대한민국 표준시)
```

1. new Date(dateString)

```jsx
new Date('May 26, 2020 10:00:00');
new Date('2020/03/26/10:00:00');
```

1. new Date(year, month[, day, hour, minute, second, millisecond])
- 연 월은 필수, 지정하지 않는 경우 1970/01/01 00:00:00(UTC)를 나타내는 Date 객체 반환

```jsx
new Date(2020,2);

new Date(2020,2,26,10,00,00,0);

new Date('2020/3/26/10:00:00:00');
```

### Date 메서드

Date.now

1970년 1월 1일 00:00:00(UTC)을 기점으로 현재 시간까지 경과한 밀리초를 숫자로 반환

```jsx
const now = Date.now();
new Date(now)
```

Date.parse

```jsx
// UTC
Date.parse('Jan 2, 1970 00:00:00 UTC'); // 86400000

// KST
Date.parse('Jan 2, 1970 09:00:00'); // 86400000

// KST
Date.parse('1970/01/02/09:00:00'); // 86400000
```

Date.UTC

1970년 1월 1일 00:00:00(UTC)을 기점으로 인수로 전달된 지정 시간까지의 밀리초를 숫자로 반환

형식은 new Date(year, month[ ,day ,hour , minute, second, milisecond]) 형식을 사용 해야 함

```jsx
Date.UTC(1970,0,2); // 86400000
Date.UTC('1970/1/2); // NaN
```

Date.prototype.getFullYear

```jsx
new Date('2020/07/24').getFullYear(); // 2020
```

Date.prototype.setFullYear

Date 객체에 연도를 나타내는 정수를 설정한다. 연도 이외에 옵션으로 월 , 일도 설정 가능

```jsx
const today = new Date();

// 년도 지정
today.setFullYear(2000);
today.getFullYear(); // 2000

// 년도/월/일 지정
today.setFullYear(1900, 0, 1);
today.getFullYear(); // 1900
```

Date.prototype.getMonth

Date 객체의 월을 나타내는 0 ~ 11의 정수를 반환 1월은 0, 12월은 11

```jsx
new Date('2020/07/24').getMonth(); // 6
```

Date.prototype.setMonth

Date 객체에 월을 나타내는 0 ~ 11의 정수를 설정한다. 1월은 0, 12월은 11이다. 월 이외에 옵션도 설정 가능

```jsx
const today = new Date();

//월 지정 
today.setMonth(0); // 1월
today.getMonth(); // 0

// 월/일 지정
today.setMonth(11,1); // 12월 1일
today.getMonth(); // 11
```

Date.prototype.setDate

```jsx
const today = new Date();

// 날짜 지정
today.setDate(1);
today.getDate(); // 1
```

Date.prototype.getDay

Date 객체의 요일(0 ~ 6 )을 나타내는 정수를 반환함

일 : 0 , 월 1, 화 2, 수 3 , 목 4, 금 5, 토 6

```jsx
new Date('2020/07/24').getDay(); // 5
```

Date.prototype.getHours

```jsx
new Date('2020/07/24/12:00').getHours(); // 12
```

Date.prototype.setHours

```jsx
const today = new Date();

//시간 지정
today.setHours(7);
today.getHours(); // 7

// 시간/분/초/밀리초 지정
today.setHours(0, 0, 0, 0); // 00:00:00:00
today.getHours(); // 0
```

Date.prototype.getMinutes

```jsx
new Date('2020/07/24/12:30').getMinutes(); // 30
```

Date.prototype.setMinutes

Date 객체에 분(0~59)을 나타내는 정수를 설정, 분 이외에 옵션으로 초, 밀리초 설정 

```jsx
const today = new Date();

today.setMinutes(50);
today.getMinutes(); // 50

today.setMinutes(5,10,99); 
today.getMinutes(); // 5
```

Date.prototype.setSeconds

Date 객체의 밀리초(0~999)를 나타내는 정수를 반환

```jsx
new Date('2020/07/24/12:30:10:150').getMilliseconds(); // 150
```