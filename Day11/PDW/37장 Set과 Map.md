# 37장 Set과 Map

## Set

Set 객체는 중복되지 않은 유일한 값들의 집합

수학적 집합을 구현하기 위한 자료구조

### 생성

```jsx
const set1 = new Set([1,2,3,3]);// [1, 2, 3]
const set2 = new Set('hello'); // '["h","e","l","o"]
```

```jsx
const uniq = array => array.filter((v,i,self)=> self.indexOf(v)=== i);

const uniq = array => [...new Set(array)];
```

### 요소 개수 확인

```jsx
const { size } = new Set([1, 2, 3, 3]); // 3
```

### 요소 추가

```jsx
const set =new Set();
set.add(1);
set.add(1).add(2);

console.log(NaN === NaN) // false
// NaN과 NaN을 같다고 평가하여서 중복 추가를 허용하지 않음
set.add(NaN).add(NaN);
```

### 요소 존재 여부 확인

```jsx
const set = new Set([1, 2, 3]);

console.log(set.has(2)); // true
console.log(set.has(4)); // false
```

### 요소 삭제

```jsx
const set = new Set([1, 2, 3]);

set.delete(2);

// 요소 일괄 삭제
set.clear();

// 요소 순회 ( 첫 번째 두번째 인수 모두 현재 순회 요소의 값)
set.forEach((v, v2, set) => console.log(v, v2, set));
/*
1 1 Set(3) {1, 2, 3}
2 2 Set(3) {1, 2, 3}
3 3 Set(3) {1, 2, 3}
*/
```

Set 객체는 이터러블이므로 for … of 문으로 순회 가능

```jsx
const set = new Set([1, 2, 3]);

// Set 객체는 Set.prototype의 Symbol.iterator 메서드를 상속받는 이터러블
console.log(Symbol.iterator in set) // true

for (const value of set) {
	console.log(value);
}

console.log([...set]); // [1, 2, 3]
const [a, ...rest] = set;
console.log(a, rest); // 1, [2, 3]
```

**교집합**

```jsx
Set.prototype.intersection = function (set) {
	const result = new Set();
	
	for (const value of set) {
		if(this.has(value)) result.add(value;
	}

	return result;
};

const setA = new Set([1, 2, 3, 4]);
const setB = new Set([2, 4]);

console.log(setA.intersection(setB)); // Set(2) [2, 4]

Set.prototype.intersection = function (set) {
	return new Set([...this].filter(v=> set.has(v)));
}
```

**합집합**

```jsx
Set.prototype.union = function (set) {
	return new Set([...this, ...set]);
}
```

**차집합**

```jsx
Set.prototype.difference = function (set) {
	return new Set([...this].filter(v => !set.has(v));
}
```

**부분 집합과 상위 집합**

```jsx
// 상위 집합인지 확인
Set.prototype.isSuperset = function (subset) {
	for(const value of subset){
		if(!this.has(value)) return false;
	}
	 return ture;
}

Set.prototype.isSuperset = function (subset) {
	const supersetArr = [...this];
	return [...subset].every(v => supersetArr.includes(v));
}
```

## Map

Map 객체는 키와 값으로 이루어진 컬렉션

### 생성

```jsx
const map1 = new Map([['key1','value1'],['key2','value2']]);

```

Map 생성자 함수는 이터러블을 인수로 전달 받아 Map 객체를 생성, 이터러블은 키와 값의 쌍으로 이루어진 요소로 구성

### 요소의 개수 확인

```jsx
const { size } = new Map([['key1','value1'],['key2','value2']]); // 2
```

### 요소 추가/취득/확인/삭제

```jsx
const map = new Map();
map.set('key1', 'value1').set('key2','value2');

map.set('key1', 'value2') // value2
```

```jsx
const map = new Map();

const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

map.set(lee, 'developer').set(kim, 'designer');
console.log(map); // Map(2) { {name: "Lee"} => "developer", {name: "Kim"} => "designer" }
console.log(map.get(lee)); // developer
console.log(map.has(lee)); // true
map.delete('kim');
```

### 요소 일괄 삭제

```jsx
map.clear();
```

### 요소 순회

```jsx
const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

const map = new Map([[lee,'developer'], [kim, 'designer']]);

map.forEach((v, k, map) => console.log(v, k , map)); // 요소 값 / 요소 키 / Map 객체

for (const key of map.keys()) {
	console.log(key);
}

for (const value of map.values()) {
	console.log(value);
}

for (const entry of map.entries()) {
	console.log(entry);
}
```