# 39장 DOM

DOM은 HTML 문서 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조이다.

## 노드

HTML 요소는 HTML 문서를 구성하는 개별적인 요소를 의미

HTML의 요소의 어트리뷰트는 어트리뷰트 노드로, 텍스트 콘텐츠는 텍스트 노도로 변환

노드 객체들로 구성된 트리 자료구조를 DOM이라 함

### 문서노드

문서 노드는 DOM 트리의 최상위에 존재하는 루트 노드로서 document 객체를 가리킴

document 객체는 브라우저가 랜더링한 HTML 문서 전체를 가리키는 객체로서 전역 객체 window의 doucument 프로퍼티에 바인딩되어있음

문서노드, document 객체는 DOM 트리의 루트 노드이므로 DOM 트리의 노드들에게 접근하기 위한 진입점 역할을 함.

### 요소노드

HTML요소를 가리키는 객체

HTML 요소 간의 중첩에 의해 부자 관계를 가지며, 부자 관계를 통해 정보를 구조화

### 어트리뷰트 노드

어트리뷰트 노드는 HTML 요소의 어트리뷰트를 가리키는 객체

어트리뷰트가 지정된 HTML 요소의 요소 노드와 연결

### 텍스트 노드

HTML 요소의 텍스트를 가리키는 객체, 요소 노드가 문서의 구조를 표현한다면 텍스트 노드는 문서의 정보를 표현

### DOM의 상속구조

DOM은 HTML 문서의 계층적 구조와 정보를 표현하는 것은 물론 노드 객체의 종류, 즉 노드 타입에 따라 필요한 기능을 프로퍼티와 메서드의 집합인 DOM API 로 제공, 이 DOM API를 통해 HTML의 구조나 내용 또는 스타일 등을 동적으로 조작 가능

## 요소 노드 취득

HTML의 구조나 내용 또는 스타일 등을 동적으로 조작하려면 먼저 요소 노드를 취득해야 함

### id를 이용한 요소 노드 취득

```jsx
<script>
	const $elem = document.getElementById('banana');
	$elem.style.color = 'red';
</script>
```

### 태그 이름을 이용한 요소 노드 취득

```jsx
<!DOCTYPE html>
<html>
	<body>
		<ul>
			<li id="apple">Apple></li>
			<li id="banana">Banana</li>
			<li id="orange">Orange</li>
		</ul>
		<script>
			const $elems = document.getElementsByTagName('li');
			[...$elems].forEach(elem => {elem.style.color = 'red';});
		</script>
	</body>
</html>
```

### class를 이용한 요소 노드 취득

```jsx
<!DOCTYPE html>
<html>
	<body>
		<ul>
			<li id="fruit apple">Apple></li>
			<li id="fruit banana">Banana</li>
			<li id="fruit orange">Orange</li>
		</ul>
		<script>
			const $elems = document.getElementsByClassName('fruit');
			[...$elems].forEach(elem => {elem.style.color = 'red';});
		</script>
	</body>
</html>
```

### CSS 선택자를 이용한 요소 노드 취득

```jsx
* { ... } // 전체 선택자
p { ... } // 태그 선택자
#foo { ... } // id 선택자
.foo { ... } // class 선택자
input[type=text] { ... } // 어트리 뷰트 선택자 
div p { ... }  // 후손 선택자
div > p { ... } // 자식 선택자
p + ul { ... } // 인접 형제 선택자
p ~ ul { ... } // 일반 형제 선택자
a:hover { ... } // 가상 클래스 선택자
a::before { ... } // 가상 요소 선택자
```

```jsx
<!DOCTYPE html>
<html>
	<body>
		<ul>
			<li class="apple">Apple></li>
			<li class="banana">Banana</li>
			<li class="orange">Orange</li>
		</ul>
		<script>
			const $elem = document.querySelector('.banana');
			$elem.style.color = 'red';
		</script>
	</body>
</html>
```

### HTMLCollection과 NodeList

DOM 컬렉션 객체인 HTMLCollection과 NodeList는 DOM API가 여러 개의 결과값을 반환하기 위한 DOM 컬렉션 객체 모두 유사 배열 객체이면서 이터러블이다. 따라서 for … of문으로 순회할 수 있으며 스프레드 문법을 사용하여 간단히 배열로 변환 할 수 있다. 

HTMLCollection과 NodeList의 중요한 특징은 노드 객체의 상태 변화를 실시간으로 반영하는 살아있는 객체

노드 객체의 상태 변경과 상관없이 안전하게 DOM 컬렉션을 사용하려면 HTMLCollection이나 NodeList 객체를 배열로 변환하여 사용하는 것을 권장

## 노드 탐색

### 자식 노드 탐색

```jsx
<!DOCTYPE html>
<html>
	<body>
		<ul id="fruits">
			<li class="apple">Apple></li>
			<li class="banana">Banana</li>
			<li class="orange">Orange</li>
		</ul>
		<script>
			const $fruits = document.getElementById('fruits');
			// childNodes 프로퍼티가 반환한 NodeList에는 요소 노드뿐만 아니라 텍스트 노드도 포함
			console.log($fruits.childNodes);
			// children 프로퍼티가 반환한 HTMLCollection에는 요소 노드만 포함
			console.log($fruits.children);
			// firstChild 프로퍼티는 텍스트 노드를 반환할 수도 있음
			console.log($fruits.firstChild); 
			// lastChild 프로퍼티는 텍스트 노드를 반환할 수도 있음
			console.log($fruits.children);
			// 요소 노드만 반환
			console.log($fruits.firstElementChild); 
			console.log($fruits.lastElementChild); 
		</script>
	</body>
</html>
```

### 자식노드 존재 확인

```jsx
<!DOCTYPE html>
<html>
	<body>
		<ul id="fruits">
		</ul>
		<script>
			const $fruits = document.getElementById('fruits');
			console.log($fruits.hasChildNodes()); // true
			console.log(!!$frutis.children.length); // 0 -> false
			console.log(!!$frutis.childElementCount); // 0 -> false
		</script>
	</body>
</html>
```

### 부모 노드 탐색

Node.prototype.parentNode 프로퍼티 사용

## 노드 정보 취득

**nodeValue**

노드 객체의 nodeValue 프로퍼티를 참조하면 노드 객체의 값을 반환한다. 노드 객체의 값이란 텍스트 노드의 텍스트이다.

**textContent**

요소 노드의 textContent 프로퍼티를 참조하면 요소 노드의 콘텐츠 영역 내의 텍스트를 모두 반환

## DOM 조작

**innerHTML**

요소 노드의 콘텐츠 영역 내에 포함된 모든 HTML 마크업을 문자열로 반환

사용자로부터 입력받은 데이터를 그대로 innerHTML 프로퍼티에 할당하는 것은 **크로스 사이트 스크립팅 공격**에 취약하므로 위험하다

**insertAdjacentHTML**

```jsx
<!DOCTYPE html>
<html>
	<body>
		<!-- beforebegin -->
		<div id="foo">
			<!-- afterbegin -->
			text
			<!-- beforeend -->
		</div>
		<!-- afterend -->
	</body>
	<script>
	const $foo = document.getElementById('foo');
	
	$foo.insertAdjacentHTML('beforebegin' , '<p>beforebegin</p>');
	$foo.insertAdjacentHTML('afterbegin' , '<p>afterbegin</p>');
	$foo.insertAdjacentHTML('beforeend' , '<p>beforeend</p>');
	$foo.insertAdjacentHTML('afterend' , '<p>afterend</p>');
	</script>
</html>

```

### 노드 생성과 추가

```jsx
<!DOCTYPE html>
<html>
	<body>
		<ul id="fruits">
			<li>Apple</li>
		</ul>
	</body>
	<script>
		const $fruits = document.getElementById('fruits);
		//1. 요소 노드 생성
		const $li = document.createElement('li');
		//2. 텍스트 노드 생성
		const textNode = document.createElement('Banana');
		//3. 텍스트 노드를 $li 요소 노드의 자식 노드로 추가
		$li.appendChild(textNode);
		//4. $li 요소 노드를 #fruits 요소 노드의 마지막 자식 노드로 추가
		$fruits.appendChild($li);
	</script>
</html>
```

```jsx
<!DOCTYPE html>
<html>
	<body>
		<ul id="fruits"></ul>
	</body>
	<script>
		const $fruits = document.getElementById('fruits);

		// DocumentFragment 노드 생성
		const $fragment = document.createDocumentFragment();
		
		['Apple','Banana','Orange'].forEach(text => {
			//1. 요소 노드 생성
			const $li = document.createElement('li');
			//2. 텍스트 노드 생성
			const textNode = document.createElement('Banana');
			//3. 텍스트 노드를 $li 요소 노드의 자식 노드로 추가
			$li.appendChild(textNode);
			//4. $li 요소 노드를 #fruits 요소 노드의 마지막 자식 노드로 추가
			$fragment.appendChild($li);
		});
		
		//5 DocumentFragment 노드를 #fruits 요소 노드의 마지막 자식 노드로 추가
		$fruits.appendChild($fragment);
	</script>
</html>
```

### 어트리뷰트

HTML 문서의 구성 요소인 HTML 요소는 여러 개의 어트리뷰트를 가질 수 있음

HTML 어트리뷰트는 HTML 요소의 시작태그에 어트리뷰트 이름=”어트리뷰트 값” 형식으로 정의

```jsx
<!DOCTYPE html>
<html>
	<body>
		<input id="user" type="text" value="ungmo2">
	</body>
	<script>
		// 요소 노드의 attribut 프로퍼티는 요소 노드의 모든 어트리뷰트 노드의 참조가 담긴 
		// NamedNodeMap 객체를 반환
		const { attributes } = document.getElementById('user');
		
		console.log(attributes.id.value); // user
		console.log(attributes.type.value); // user
		console.log(attributes.value.value); // user
	</script>
	</body>
</html>
```

**HTML 어트리뷰트 조작**

```jsx
<!DOCTYPE html>
<html>
	<body>
		<input id="user" type="text" value="ungmo2">
	</body>
	<script>
		const $input = document.getElementById('user');
		
		const inputValue = $input.getAttribute('value'); // ungmo2
	
		$input.setAtttribute('value' , 'foo');
		
		if($input.hasAttribute('value')){
			$input.removeAttribute('value');
		}
	</script>
	</body>
</html>
```

**HTML 어트리뷰트 vs DOM 프로퍼티**

**HTML 어트리뷰트**

HTML 어트리뷰트의 역할은 HTML 요소의 초기 상태를 지정하는 것, HTML 어트리뷰트 값은 HTML 요소의 초기상태를 의미하며 변하지 않는다.

**DOM 프로퍼티**

사용자가 입력한 최신 상태는 HTML 어트리뷰트에 대응하는 요소 노드의 DOM 프로퍼티가 관리 DOM 프로퍼티는 사용자의 입력에 의한 상태 변화와 반응하여 언제나 최신 상태 유지

요소 노드는 2개의 상태, 즉 초기 상태와 최신 상태를 관리해야 한다. 요소 노드의 초기 상태는 어트리뷰트 노드가 관리하고, 요소 노드의 최신 상태는 DOM 프로퍼티가 관리한다.

```jsx
<!DOCTYPE html>
<html>
	<body>
		<input id="user" type="text" value="ungmo2">
	</body>
	<script>
		const $input = document.getElementById('user');
		// 사용자 입력에 따른 최신 상태 값 취득 , value 프로퍼티 값은 사용자의 입력에 의해 동적 변경
		$input.oninput = () => {
			console.log('value 프로퍼티 값', $input.value);
		};
		// getAttribute 메서드로 취득한 HTML 어트리뷰트 값, 즉 초기 상태 값은 변하지 않고 유지
		console.log('value 어트리뷰트 값', $input.getAttribute('value'));
	</script>
	</body>
</html>
```

```jsx
<!DOCTYPE html>
<html>
	<body>
		<input id="user" type="text" value="ungmo2">
	</body>
	<script>
		const $input = document.getElementById('user');
		// id 어트리뷰트와 id 프로퍼티는 사용자 입력과 관계없이 항상 동일한 값으로 연동
		$input.id = 'foo';
		console.log($input.id); // foo
		console.log($input.getAttribute('id')); // foo
	</script>
	</body>
</html>
```

사용자 입력에 의한 상태 변화와 관계있는 DOM 프로퍼티만 최신 상태 관리 

**data 어트리뷰트와 dataset 프로퍼티**

data 어트리뷰트와 dataset 프로퍼티를 사용하면 HTML 요소에 정의한 사용자 정의 어트리뷰트와 자바스크립트 간에 데이터를 교환할 수 있음

data 어트리뷰트는 data-user-id, data-role 과 같이 data- 접두사 다음에 임의의 이름을 붙여 사용

```jsx
<!DOCTYPE html>
<html>
<body>
	<ul class="users">
		<li id="1" data-user-id="7621" data-role="admin">Lee</li>
		<li id="2" data-user-id="9524" data-role="subscriber">Kim</li>
	</ul>
	<script>
		<script>
        const users = [...document.querySelector('.user').children];
        const user = users.find(user => user.dataset.userId === '7621')
        console.log(user.dataset.role); // admin
        user.dataset.role = 'subscriber';
        console.log(user.dataset) // DOMStringMap {userId: '7621', role: 'subscriber'}
    </script>
	</script>
</body>
</html>
```

## 스타일

**인라인 스타일 조작**

```jsx
<div style="color: red">Hello World</div>

$div.style.backgroundColor = 'yellow';
$div.style['background-color'] = 'yellow'; 
```

**클래스 조작**

className

Element.prototype.className 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티로서 HTML 요소의 class 어트리뷰트 값을 취득하거나 변경한다.

classList

Element.prototype.classList 프로퍼티는 class 어트리뷰트의 정보를 담은 DOMTokenList 객체를 반환