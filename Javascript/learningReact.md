![http://image.kyobobook.co.kr/images/book/xlarge/494/x9791162244494.jpg](http://image.kyobobook.co.kr/images/book/xlarge/494/x9791162244494.jpg)

---

# 3. 자바스크립트를 활용한 함수형 프로그래밍

## 3.1. 함수형 프로그래밍 개요

함수형 프로그래밍 기법은 리액트 뿐 아니라 리액트 생태계를 이루는 여러 라이브러리의 근간이다.

함수가 1급 시민이 되면 변수에 함수를 대입할 수 있고, 함수를 다른 함수에 인자로 넘길 수 있으며, 함수에서 함수를 만들어서 반환할 수 있어야 한다.

자바스크립트에서는 함수가 1급 시민이기 때문에, 자바스크립트가 함수형 프로그래밍을 지원한다고 말할 수 있다. 1급 시민이라는 말은 정수나 문자열 같은 다른 일반적인 값과 마찬가지로 함수를 취급할 수 있다는 뜻이다. 

- 이처럼 함수를 객체에 넣을 수 있다.

```jsx
const obj = {
	message: '안녕',
	log(message) {
		console.log(message);
	}
}

obj.log(obj.message); // 안녕
```

- 이처럼 배열에 함수를 넣을 수 있다.

```jsx
const array = [
	"안녕",
	message => console.log(message),
]

array[1](array[0]); //안녕
```

- 이처럼 함수를 다른 함수에 인자로 넘길 수 있다.

```jsx
const insideFn = logger => {
	logger("안녕");
};

const fn = message => console.log(message)
insideFn(fn); //안녕
```

- 이처럼 함수가 함수를 반환할 수 있다.(createScream함수는 함수를 반환한다)

```jsx
const createScream = function(logger) {
	return function(message) { 
		logger(message.toUpperCase() + "!!!");
	};
};

const scream = createScream(message => console.log(message));

scream('hello'); // HELLO!!!
```

특히, 함수가 함수를 인자로 받는 경우와 함수가 함수를 반환하는 경우를 `고차함수` 라고 부른다.

```jsx
// 위 고차함수를 화살표 함수로 표현
const createScream = logger => message => {
	logger(message.toUpperCase() + "!!!");
};
```

이처럼 함수에 2개 이상의 화살표가 있다면 고차 함수를 사용하고 있다는 뜻이다.

## 3.2 명령형 프로그래밍과 선언적 프로그래밍 비교

프로그래밍 패러다임을 크게 `선언적 프로그래밍`과 `명령형 프로그래밍`으로 나눌 수 있다.

함수형 프로그래밍은 `선언적 프로그래밍` 의 방법 중 하나이다.

- `선언적(declarative) 프로그래밍`은 ~~필요한 것을 달성하는 과정을 하나하나 기술하는 것~~보다 필요한 것이 어떤 것인지를 기술하는 것에 더 방점을 두고 애플리케이션 구조를 세워나가는 프로그래밍 스타일이다.
    - 선언적 프로그래밍의 코드 구문은 어떤 일이 발생해야 하는지에 대해 기술하고, 실제로 그 작업을 처리하는 방법은 추상화를 통해 아랫단에 감춰진다.
    - 선언적 접근 방식이 더 읽기 쉽고, 그렇기 때문에 더 추론하기 쉽고, 그 애플리케이션의 규모를 확장하는 것도 더 쉽다.
- `명령형(imperative) 프로그래밍` 은 코드로 원하는 결과를 달성해 나가는 과정에만 관심을 두는 프로그래밍 스타일이다.

## 3.3 함수형 프로그래밍의 개념

함수형 프로그래밍의 핵심 개념으로 불변성(immutability), 순수성(purity), 데이터 변환(transformation), 고차 함수, 재귀(recursion) 등이 있다.

### 3.3.1 불변성

함수형 프로그래밍에서는 데이터가 변할 수 없다.

그래서 원본 데이터 구조를 변경하는 대신 그 데이터 구조의 복사본을 만들되 그중 일부를 변경한다.

 그리고 원본 대신 변경한 복사본을 사용해 필요한 작업을 진행한다.

[객체]

- Object.assign을 사용함으로써 1depth의 깊은 복사를 하였고, 이 덕분에 원본에 영향을 미치지 않고 불변성을 유지할 수 있다.

```jsx

const color_lawn =  {
	title: "잔디",
	color: "#00F00",
	rating: 0,
};

const rateColor = (color, rating) => {
	return Object.assign({}, color, {rating: rating});
}

console.log(rateColor(color_lawn, 5).rating); // 5
console.log(color_lawn.rating); // 0
```

- 위 코드는 객체 스프레드 연산자를 활용하여 불변성을 유지하도록 리팩토링할 수도 있다.
    - 스프레드 연산자를 사용해 원본(color)을 새로운 객체 안에 복사한 다음에 프로퍼티(rating)를 덮어쓴다.

```jsx
const ratecolor = (color, rating) => ({
	...color,
	rating
});
```

[배열]

- 원본 배열을 변화시키지 않고 유지하기 위해 Array.concat을 사용할 수 있다.

```jsx

let list = [
	{title: '빨강'},
];

const addColor = (title, array) => array.concat({title});

console.log(addColor('녹색', list).length); // 2
console.log(list.length); // 1
```

- 위 코드는 배열 스프레드 연산자를 사용해 불변성을 유지하며 배열을 복사할 수 있다.
    - 위 함수는 원본 list의 원소들을 새 배열에 복사하고, title 파라미터로 받은 값을 title 프로퍼티로 하는 객체를 새 배열 뒤에 추가한다.

```jsx
const addColor = (title, list) => [...list, {title}];
```

### 3.3.2 순수 함수

순수 함수(Pure Functions)는 파라미터에 의해서만 반환값이 결정되는 함수를 뜻한다. 이는 함수형 프로그램의 핵심 개념 중 하나이다.

- 순수함수에는 부수 효과(side effect)가 없다.
    - 부수 효과란 전역 변수를 설정하거나, 함수 내부나 애플리케이션에 있는 다른 상태를 변경하는 것을 말한다.
    - 순수 함수는 인수를 변경 불가능한 데이터로 취급한다.
- 순수함수 규칙
    1. 순수 함수는 파라미터를 최소한 하나 이상 받아야 한다.
    2. 순수 함수는 값이나 다른 함수를 반환해야 한다.
    3. 순수 함수는 인자나 밖에 있는 다른 변수를 변경하거나, 입출력을 수행해서는 안된다.

- 리액트에서는 UI를 순수 함수로 표현한다.
- 순수 함수를 사용하면 애플리케이션의 상태에 영향을 미치지 않기 때문에 코딩이 편해진다.

다음은 DOM을 변경하는 순수하지 않는 함수의 예시이다.

- 이 함수는 함수나 값을 반환하지 않으며(규칙2 위반), DOM을 변경하는 부수 효과를 발생시키기(규칙3 위반) 때문에, 순수하지 않은 함수이다.

```jsx
function Header(text) {
	let h1 = document.createElement('h1');
	h1.innerText = text;
	document.body.appendChild(h1);
}

Header("안녕");
```

- 리액트 등에서 UI로 사용할 순수함수의 예시는 다음과 같다. 부수 효과를 발생시키지 않고 엘리먼트를 반환한다. 이 함수는 엘리먼트를 만드는 일만 책임지며, DOM을 변경하는 책임은 애플리케이션의 다른 부분이 담당해야 한다.

```jsx
const Header = (props) => <h1>{props.title}</h1>
```

### 3.3.3 데이터 변환

- 함수형 프로그래밍은 한 데이터를 다른 데이터로 변환하는 것이 전부다.
- 함수형 프로그래밍은 함수를 사용해 원본을 변경한 복사본을 만들어낸다.
    - 그런 식으로 순수 함수를 사용해 데이터를 변경하면, 코드가 덜 명령형이 되고 그에 따라 복잡도도 감소한다.
    

자바스크립트 내장 함수를 사용하여 데이터 변환하여 다른 데이터를 만들어낼 수 있다.

새 값을 반환하는 Array.join, Array.filter, Array.map, Array.reduce, Array.reduceRight

```jsx
const ages = [21,18,42,40,64,63,34];

const max = ages.reduce((max, value) => (value > max ? value : max), 0);

console.log(max)
```

```jsx
const colors = ['red', 'red', 'green', 'blue', 'green'];

const uniqueColors = colors.reduce(
  (unique, color) =>
    unique.indexOf(color) !== -1 ? unique : [...unique, color],
  []
);

console.log(uniqueColors); // ["red", "green", "blue"]
```

### 3.3.4 고차 함수

고차 함수는 다른 함수를 조작할 수 있는 함수다. 

고차함수는 다른 함수를 인자로 받을 수 있거나 함수를 반환할 수 있고, 때로는 그 2가지를 모두 수행한다.

예를 들어, Array.map, Array.filter, Array.reduce는 다른 함수를 인자로 받기 때문에, 모두 고차 함수다.

다른 함수를 반환하는 고차 함수는 자바스크립트에서 비동기적인 실행 맥락을 처리할 때 유용하다. 함수를 반환하는 고차 함수를 쓰면 필요할 대 재활용할 수 있는 함수를 만들 수 있다.

- 커링
    - `커링(Currying)` 은 고차 함수 사용법과 관련한 함수형 프로그래밍 기법이다.
    - 커링은 어떤 연산을 수행할 때 필요한 값 중 일부를 저장하고, 나중에 나머지 값을 전달받는 기법이다. 이를 위해 다른 함수를 반환하는 함수를 사용하며, 이를 커링된 함수(Curried fucntion) 라고 부른다.
    

### 3.3.5 재귀

재귀는 비동기 프로세스에서도 잘 작동하는 또 다른 함수형 기법이다. 함수는 필요할 때 자기 자신을 다시 호출할 수 있다. 

### 3.3.6 합성

함수형 프로그램은 로직을 구체적인 작업을 담당하는 여러 작은 순수 함수로 나눈다. 그 과정에서 언젠가는 모든 작은 함수를 한데 합칠 필요가 있다. 

합성 방법으로 체이닝 등이 있으나, 함수를 더 큰 함수로 조합해주는 compose와 같은 커스텀 함수를 사용할 수 있다.

```jsx
const compose = (...fns) => (arg) => 
	fns.reduce((composed, f) => f(composed), arg);
```

compose는 여러 함수를 인자로 받아서 한 함수를 결과로 내놓는다. 

- 이 구현은 스프레드 연산자를 사용해 인자로 받은 함수들을 fns라는 배열로 만든다.
- 그 후 compose는 arg라는 인자를 받는 함수를 반환한다.
- 이렇게 반환된 화살표 함수에 나중에 누군가 인자를 전달해 호출하면, fns 배열의 reduce를 호출하면서 arg로 받은 값을 전달한다.
- arg 값은 reduce의 초깃값이 되고, 각 이터레이션마다 배열의 각 원소(함수)와 이전 값을 변환 함수를 사용해 축약한 값을 전달한다.
- 이때 reduce의 변환 함수는 이전 이터레이션의 결괏값인 composed와 f를 인자로 받아서 f에 composed를 적용해 반환한다. 언젠가는 마지막 함수가 호출되며 최종 결과를 반환한다.

```jsx
const both = arg => funcSecond(funcFirst(arg));

// 위와 같은 구문은 이해하기 어렵고 그로 인해 유지 보수나 대규모 확장이 어렵다.
// 따라서 아래와 같이 함수를 더 큰 함수로 조합해주는 compose함수로 리팩토링한다.

const both = compose(
	funcFirst,
	funcSecond
);
```

- compose 함수 예시

```jsx
const compose = (...fns) => (arg) => 
	fns.reduce((composed, f) => f(composed), arg);

const funcFirst = (word) => `{${word}}`

const funcSecond = (word) => `[${word}]`

const both = compose(
	funcFirst,
	funcSecond
);

console.log(both('hello')) // [{hello}]
```

# 4. 리액트의 작동 원리

## 4.1 페이지 설정

- React는 뷰를 만들기 위한 라이브러리이다.
- ReactDOM은 UI를 실제로 브라우저에 렌더링할 때 사용하는 라이브러리다.

## 4.2 리액트 엘리먼트

- 전통적으로 웹사이트는 독립적인 HTML 페이지들로 만들어졌다. 사용자가 페이지 사이트를 내비게이션 함에 따라 브라우저는 매번 다른 HTML 문서를 요청해서 로딩할 수 있었다. AJAX(Asynchronous Javascript and XML)가 생기면서 단일 페이지 애플리케이션(SPA, Single Page Application)이 생겼다. 브라우저가 AJAX를 사용해 아주 작은 데이터를 요청해서 가져올 수 있게 됨에 따라 이제는 전체 웹 애플리케이션이 한 페이지로 실행되면서 자바스크립트에 의존해 사용자 인터페이스를 갱신하게 됐다.
- `DOM API`는 브라우저의 DOM을 변경하기 위해 자바스크립트가 사용할 수 있는 객체의 모음이다.
    - 브라우저의 DOM은 DOM 엘리먼트로 이뤄진다.
    - 마찬가지로 React DOM은 리액트 엘리먼트로 이뤄진다. 리액ㅇ트 엘리먼트는 브라우저 DOM을 만드는 방법을 알려주는 명령이다.
- 리액트는 브라우저 DOM을 갱신해주기 위해 만들어진 라이브러리다. 리액트가 모든 처리를 대신 해주기 때문에 더 이상 SPA를 더 효율적으로 만들기 위해 여러 복잡한 내용을 신경쓸 필요가 없다. 리액트에서는 코드로 DOM API를 직접 조작하지 않는다. 대신 리엑트에게 어떤 UI를 생성할지 지시하면, 리액트가 우리 명령에 맞춰 원소 렌더링을 조절해준다.

- React.createElement를 사용해 h1을 표현하는 리액트 엘리먼트를 만들면 다음과 같다.

```jsx
React.createElement("h1", {id: "recipe-0"}, "떡볶이")
```
