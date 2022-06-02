# 31장 RegExp

## 정규 표현식이란

- 정규 표현식은 문자열 대상으로 패턴 매칭 기능을 제공

```jsx
const tel = '010-1234-578팔'

const regExp = /^\d{3}-\d{4}-\d{4}$/';

regExp.test(tel); // false
```

## 정규 표현식의 생성

- / → 시작 종료 기호

```jsx
const target = 'Is this all there is';

// 패턴 is
// flags: 정규표현식의 플래그(g, i, m, u, y)
const regexp = /is/i; 

regexp.test(target);
```

```jsx
const target = 'Is this all there is?';

const regexp = new RegExp(/is/i); // ES6

regexp.test(target);
```

## RegExp 메서드

RegExp.prototype.exec

exec 메서드는 인수로 전달 받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 배열로 반환한다.

```jsx
const target = 'Is this all there is?';
const regExp = /is/;

regExp.exec(target); // ["is", index :5, input: "Is this all there is", groups: undefined]
```

exec 메서드는 문자열의 모든 패턴을 검색하는 g 플래그를 지정해도 첫번 째 매칭 결과만을 반환한다.

RegExp.prototype.test

test 메서드는 인수로 전달 받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 불리언 값으로 반환

String.prototype.match

String 표준 빌트인 객체가 제공하는 match 메서드는 대상 문자열과 인수로 전달받은 정규 표현식과의 매칭 결과를 배열로 반환

```jsx
const target = 'Is this all there is?';
const regExp = /is/;

target.match(regExp);// ["is", index :5, input: "Is this all there is", groups: undefined]

const regExp = /is/g;

target.match(regExp); // ["is", "is"]
```

## 플래그

- 정규 표현식의 검색 방식을 설정하기 위해 사용
- 종류
    - i : 대소문자를 구별하지 않고 패턴을 검색
    - g: 대상 문자열 내에서 패턴과 일치하는 모든 문자열을 전역 검색
    - m: 문자열의 행이 바뀌더라도 패턴 검색을 계속한다.
    

```jsx
const target = 'Is this all there is?';

// 대소문자를 구별하여 한번만 검색
target.match(/is/);// ["is", index :5, input: "Is this all there is", groups: undefined]

// 대소문자를 구별하지 않고 한 번만 검색
target.match(/is/i);// ["Is", index :0, input: "Is this all there is", groups: undefined]

// 대소문자를 구별하여 전역 검색
target.match(/is/g); // ["is","is"]

// 대소문자를 구별하지 않고, 전역 검색
target.match(/is/ig); // ["Is","is","is"]
```

## 패턴

- 일정한 규칙을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어
- 정규 표현식은 패턴과 플래그로 구성
- / 로 열고 닫으며 문자열의 따옴표는 생략

**임의의 문자열 검색**

```jsx
const target = 'Is this all there is?';

const regExp = /.../g;

target.match(regExp); // ["Is " , "thi", "s a", "ll ", "the" , "re ", "is?"]
```

**반복 검색**

{m, n} 은 앞선 패턴이 최소 m번, 최대 n번 반복되는 문자열을 의미함 

, 뒤에는 공백이 없어야함에 주의

```jsx
const target = 'A AA B BB Aa Bb AAA';

const regExp = /A{1,2}/g;

target.match(regExp); // ["A", "AA", "A", "AA", "A"]
```

+는 {1,}과 같다.

```jsx
const target = 'A AA B BB Aa Bb AAA';

const regExp = /A+/g;

target.match(regExp); // ["A", "AA", "A", "AAA"]
```

?는 앞선 패턴이 최대 한 번(0번 포함) 이상 반복되는 문자열을 의미

```jsx
const target = 'color colour';

const regExp = /colou?r/g;

target.match(regExp); // ["color", "colour"]
```

**OR 검색**

```jsx
const target = 'A AA B BB Aa Bb';

const regExp = /A|B/g;

target.match(regExp); // ["A", "A", "A", "B", "B", "B", "A", "B"] 
```

```jsx
const target = 'A AA B BB Aa Bb';

const regExp = /A+|B+/g;

target.match(regExp); // ["A", "AA", "B" , "BB", "A", "B"]
```

[] 내의 문자는 or로 동작한다.

```jsx
const target = 'A AA B BB Aa Bb';

const regExp = /[AB]+/g;

target.match(regExp); // ["A", "AA", "B" , "BB", "A", "B"]
```

범위를 지정하려면 [] 내에 - 를 사용한다.

```jsx
const target = 'A AA BB ZZ Aa Bb';

const regExp = /[A-Z]+/g;

target.match(regExp); // ["A", "AA", "ZZ", "A", "B"]

const target = 'AA BB Aa Bb 12';

const regExp = /[A-Za-z]+/g;

target.match(regExp); // ["AA", "BB", "Aa", "Bb"]

const target = 'AA BB 12,345';

const regExp = /[0-9]+/g;

target.match(regExp); // ["12", "345"]
```

\d는 숫자를 의미, \D는 문자를 의미한다.

\w는 알파벳, 숫자,언더스코어를 의미한다. \W는 \w 외의 것들을 의미한다

NOT 검색

[]안에 ^는 not의 의미를 갖는다.

```jsx
const target = "AA BB 12 Aa Bb";

const regExp = /[^0-9]+/g;

target.match(regExp); // ["AA BB ", "Aa Bb"];
```

시작 위치로 검색

[] 밖에 ^는 문자열의 시작을 의미한다.

```jsx
const target = 'https://poiemaweb.com";

const regExp = /^https/;

regExp.test(target); // true;
```

마지막 위치로 검색

$는 문자열의 마지막을 의미

```jsx
const target = 'https://poiemaweb.com";

const regExp = /com$/;

regExp.test(target); // true;
```

## 자주 사용하는 정규표현식

특정 단어로 시작하는지 검사

```jsx
const url = 'https://example.com';

/^https?:\/\//.test(url);
```

특정단어로 끝나는 지 검사

```jsx
const fileName = 'index.html';

/html$/.test(fileName);
```

숫자로만 이루어진 문자열인지 검사

```jsx
const target = '12345';
/^\d+$/.test(target)
```

하나 이상의 공백으로 시작하는 검사

\s는 여러 가지 공백문자(스페이스, 탭 등)을 의미함 → \s = [\t\r\n\v\f]와 같은 의미

```jsx
const target = ' Hi!';
/^[\s]+/.test(target);
```

아이디로 사용 가능한지 검사

알파벳 대소문자 또는 숫자로 시작하고 끝나며 4~10자리인지 검사

```jsx
const id = 'abc123';

/^[A-Za-z0-9]{4,10}/.test(id);
```

메일 주소 형식에 맞는지 검사

```jsx
const email = "ungmo2@gmail.com"
/^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/.test(email);
```