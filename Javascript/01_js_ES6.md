## String
ES2015 string에 새로운 메서드들
- startsWith
- endsWtih
- includes
```javascript
let str="hello world!"
let startStr= "hello";
let endStr="orld!"
console.log("start test ", str.startsWith(startStr));
console.log("end test ", str.endsWith(endStr));
console.log("include test ", str.includes("!"));
```
## Array
### 1. for of - 순회하기
- for문
```javascript
var data = [1,2,undefined,NaN,null,""];
for(var i=0;i<data.length;i++){
  console.log(i)
}
```

- forEach 순회
```javascript
var data = [1,2,undefined,NaN,null,""];
data.forEach(function(value){
  console.log(value);
});
```

- for in
```javascript
var data = [1,2,undefined,NaN,null,""];
for(let idx in data) {
  console.log(data[idx]);
}
```
for in의 문제점: for in은 의도와 달리 오브젝트에서 자신이 가지고 있는 객체 이외에 
프로토타입 객체를 이용하여 상위의 추가된 객체도 포함하여 나타내는 문제가 있다.
그래서 array에서 for in을 절대 사용하지 않는다.

- for of
```javascript
var data = [1,2,undefined,NaN,null,""];
for(let value of data) {
  console.log(value);
}
```
for in으로 인한 실수를 줄이기 위해 for of가 나왔다. forEach외에도 for of를 사용하여 배열을 순회할 수 있다.

### 2. spread operator - 배열의 복사
spread operator 펼침연산자

```javascript
let pre = ["apple","orange",100];
let newData = [...pre];
console.log(pre, newData);
```
'...객체'는 해당 객체의 참조를 끊고 메모리의 새로운 공간에 새 배열을 복사한 것이다.
위 코드에서 pre와 newData는 동일한 데이터를 갖고 있지만, 서로 같은 참조를 유지하진 않는다.
완전히 복사한 것이다.

```javascript
let pre = [100,200,"hello",null];
let newData=[0,1,2,3,...pre,4];
console.log(newData)
//output : [0, 1, 2, 3, 100, 200, "hello", null, 4]
```

```javascript
function sum(a,b,c){
  return a+b+c;
}
let pre = [100,200,300];
console.log(sum(...pre));
```
펼침연산자를 이용하여 함수 sum에 array 값을 펼쳐서 매개변수로 할당하는 것이 쉬워졌다.

### 03. from 메서드로 진짜 배열 만들기

함수에 인자값이 없어도 함수 내부에 지역변수와 같은 객체인 arguments를 이용하여
외부에서 전달된 인자값을 arguments로 배열과 비슷한 형태로 전달된다.
arguments는 권장되지는 않으나 가변적인 parameter가 들어오는 경우 유용하기에 가끔 사용한다.
```javascript
function addMark() {
  let newData=[];
  for(let i=0; i<arguments.length;i++){
      newData.push(arguments[i]+"!");
  }
  console.log(newData);
}
addMark(1,2,3,4,5)
//["1!", "2!", "3!", "4!", "5!"]
```

***arguments는 배열과 흡사하지만 배열은 아니다. 이러한 가짜 배열을 진짜 배열로 만드려면
from 문을 사용하면 된다.***
```javascript
let newArray = Array.from(arguments);
//arguments로부터 배열을 만들어서 newArray에 저장한다.
```
```javascript
function addMark() {
  let newArray = Array.from(arguments);
  let newData = newArray.map(function(value){
    return value + "!";
  })
  console.log(newData);
}
addMark(1,2,3,4,5)
//["1!", "2!", "3!", "4!", "5!"]
```

Array인지 NodeList인지 정확한 타입 확인할 때 toString.call() 사용할 수 있다.
```js
console.log(toString.call(list));
console.log(typeof list);
```

- filter, includes, from을 사용해서 문자열 'e'가 노드로 구성된 배열을 만들어서 반환하기
```js
function print() {
  const list = document.querySelectorAll("li");
  const listArray = Array.from(list); //li노드로 구성된 배열
  const eArray = listArray.filter(value => value.innerText.includes("e"))
  return eArray.length;
}
console.log(print());
```

## Object
### 간단히 객체생성하기

key와 value값이 일치하면 key:value가 아니라 key만 써서 축약하여 object 선언할 수 있다.


##Destructuring
### Destructuring Array
let [jisu,, jung] = data; 
```js
let data = ["crong", "honux", "jk", "jinny"];

//이렇게 할 수 있지만,
let jisu = data[0];
let jung = data[2]; 

//이렇게 destructuring하여 위와 같은 결과를 낼 수 있다. 
let [jisu,, jung] = data;  

console.log(jisu, jung)
```

### Destructuring Object

```js
let obj = {
  name:"crong",
  address:"Korea",
  age:10
}

let {name, age} = obj;
console.log(name,age);

let {name:myName, age:myAge} = obj;
console.log(myName,myAge);
```
let {name, age} = obj;
새로 이름을 붙일 수도 있다.
let {name:myName, age:myAge} = obj;

### Destructuring 활용 JSON파싱
```js
let news = [
  {
    "title": "sbs",
    "imgurl": "http:/asdfasdfa.com",
    "newslist": [
      "뉴스1", "뉴스1"
    ]
    
  },
  {
    "title": "mbc",
    "imgurl": "http://asdfsadf.com",
    "newslist": [
      "dsafasd","sdafwef"]
    
  }
]
```
```js
let [, mbc]=news;
let {title, newslist} = mbc;
console.log(title, newslist)
```
```js
let [, {title, newslist}] = news;
console.log(title, newslist)
```

###Destructuring 활용_Event객체전달
매겨변수에도 destructuring 활용할 수 있다.
```js
]

function getNewsList([,{newslist}]) {
  console.log(newslist);
}

getNewsList(news);
```

event 객체를 다 받는 것이 아니라, destructuring하여
원하는 부분만 받는다.
```js
document.querySelector("div").addEventListener("click", function({type,target}){
  console.log(type, target.tagName);
})
```

## Set & WeakSet
set은 중복 없이 유일한 값만 저장된다. 이미 존재하는지 체크할 때 유용하다.
```js
let mySet = new Set();
console.log(toString.call(mySet));
//"[object Set]"

mySet.add("crong");
mySet.add("hary");
mySet.add("crong");
mySet.add("wow");
mySet.delete("wow");

console.log(mySet.has("crong"));
//true

mySet.forEach(function(v){
  console.log(v)
})
//"crong"
//"hary"
```

### WeakSet 으로 효과적으로 객체타입저장하기
WeakSet은 참조를 가지고 있는 객체만 저장 가능하다.
객체형태를 중복없이 저장하려고 할 때 유용하다.
``js
let arr = [1,2,3,4];
let arr2 = [5,6,7,8];

let ws = new WeakSet();
ws.add(arr);
// ws.add(111);
// ws.add("111");
ws.add(arr2);
arr=null;
console.log(ws);
console.log(ws.has(arr2));
```

## Map & WeakMap
### Map & WeakMap 추가정보를 담은 객체저장하기
Array에서 특정 용도로 변경한 것이 set, weakset이고
object에서 특정 용도로 변경한 것이 map, weakmap이다.

map은 key/value 형태이다.
```js
let wm = new WeakMap();
let myfun = function(){
};
//이 함수가 얼마나 실행됐지를 알려고 할 때

wm.set(myfun, 0);
console.log(wm);

let count=0;
for(let i=0; i<10; i++){
  console.log(wm.get(myfun));

  count++;
  wm.set(myfun, count);
  
}
```

### WeakMap 클래스 인스턴스 변수 보호하기
WeakMap 활용

weakmap에서 객체에 추가 정보를 담고, class는 인스턴스 변수를 가지고 있지 않다.
단점은 class 밖의 전역공간에 보관한다는 것이다.
private한 변수를 직접 만들어서 쓸 때는 weakmap을 이용하여 보관하면 효율적이다.

```js
const wm = new WeakMap(); //weakMap이 전역공간에 있을 때 효율적으로 활용가능

function Area(height, width) {
//   this.height =height;
//   this.width = width;
  wm.set(this, {height, width});
}

Area.prototype.getArea = function(){
//   return this.height * this.width;
  const {height, width} = wm.get(this);
  return height*width;
  
}

let myarea = new Area(10,20);
console.log(myarea.getArea()); //여기까지 접근되나
console.log(myarea.height); //그 내부 변수에는 접근 안되도록
```


## Template
### Template처리

json으로 응답을 받고, javascript object로 변환한 후에 어떠한 데이터처리 조작을 
한 후에 dom에 추가한다.
데이터+HTML 문자열의 결합이 필요하기 때문이다.

```js
const data = [
  {
    name: 'coffee-bean',
    order: true,
    items : ['americano', 'milk']
  },
  {
    name: 'starbucks',
    order: false
  }
]

const template = `<div>welcome ${data[0].name}`;
console.log(template)
```

### Tagged Template literals

```
const data = [
  {
    name: 'coffee-bean',
    order: true,
    items : ['americano', 'milk']
  },
  {
    name: 'starbucks',
    order: false
  }
]

function fn(tags, name, items) {
  if(typeof items === "undefined") {
    items = "주문가능한 상품이 없습니다";
  }
  return (tags[0] + name + tags[1] + items + tags[2])
}

const template = fn`<div>welcome ${data[1].name} </div><h2>주문가능항목</h2> <div>${data[1].items}</div>`;
console.log(template)
```
//output: "<div>welcome starbucks </div><h2>주문가능항목</h2> <div>주문가능한 상품이 없습니다</div>"

```
const data = [
  {
    name: 'coffee-bean',
    order: true,
    items : ['americano', 'milk']
  },
  {
    name: 'starbucks',
    order: false
  }
]

function fn(tags, name, items) {
  if(typeof items === "undefined") {
    items = "주문가능한 상품이 없습니다";
  }
  return (tags[0] + name + tags[1] + items + tags[2])
}

data.forEach((v) => {
  let template = fn`<div>welcome ${v.name} </div><h2>주문가능항목</h2> <div>${v.items}</div>`;
  console.log(template)
})
```

## function
### Arrow function 활용
- CallBack 콜백함수란
CallBack 함수란 이름 그대로 나중에 호출되는 함수를 말한다.
콜백함수라고 해서 그 자체로 특별한 선언이나 문법적 특징을 가지고 있지는 않다.
콜백함수도 일반적인 자바스크립트 함수일 뿐이다.
콜백 함수는 코드를 통해 명시적으로 호출하는 함수가 아니라, 개발자는 단지 함수를 등록하기만 하고, 어떤 이벤트가 발생했거나 특정 시점에 도달했을 때 시스템에서 호출하는 함수를 말한다.
즉 콜백함수는 콜백함수라는 유니크한 문법적 특징을 가지고 있는 것이 아니라, 호출방식에 의한 구분이다.

Callback 함수를 사용하는 이유는, 자바스크립트에서 비동기적 프로그래밍을 할수 있기 때문이다.
이 콜백함수기법은 자바스크립트에서 가장 오래된 비동기적 메커니즘이라고 한다.

* 비동기적 테크닉 : 소중한 싱글스레드의 멈춤을 방지한다. 즉 블록킹을 방지하여 싱글스레드가 논블록킹으로 동작하게 한다.
- 비동기적 테크닉을 사용하는 경우
1.사용자 이벤트 처리
브라우저 화면에서 발생하는 사용자의 이벤트는 예측이 불가능하다.
따라서 이런 화면이벤트를 관리담당하는 녀석에게 우리는 특정이벤트가 발생할 때 호출을 원하는 내용을 callback 함수에 전달하게 된다.
2.네트워크 응답 처리
화면단에서 서버에게 요청을 보냈을 때, 그 응답이 언제 올지 알 수 없다.
따라서 이런 서버에 대한 응답처리 등도 비동기적으로 처리해야 한다.
3.파일을 읽고 쓰는 등의 파일 시스템 작업
4.의도적으로 시간 지연을 사용하는 기능(알람 등)

위와 같이 스레드의 블록킹을 야기하는 작업은 필수적으로 비동기적 프로그래밍을 해야 한다.

```js
let newArr = [1,2,3,4,5].map(function(value,index,object){
  return value*2;
})

console.log(newArr)
```
위와 같이 하면 기니까 아래 처럼 Arrow functino 사용 가능
```js
let newArr = [1,2,3,4,5].map((v,i,o) => {
  return v*2;
})

console.log(newArr)
```

ES6에서는 아래처럼 return을 생략할 수 있다.
```js
let newArr = [1,2,3,4,5].map((v,i,o) => (v*2))

console.log(newArr)
```

### Arrow function 의 this context
callback함수를 넣어주었는데 bind없이 this가 가리키는 부분이 

bind(this)를 해주지 않으면 this.메서드()는 해당 엘리먼트의 function이 아니다.
아래 코드에서 this는 div element를 가리키므로, bind(this) 해주어야 한다.
```js
const el = document.querySelector("div");

const myObj = {
  register() {
    el.addEventListener("click", function(evt) {
      this.printData(evt.target);
    }.bind(this))
  },
  
  printData(el) {
    console.log("clicked!", el.innerText);
  }
}

myObj.register();
```

콜백함수를 arrow로 쓴다면 
```js
const el = document.querySelector("div");

const myObj = {
  register() {
    el.addEventListener("click", (evt) => {
      this.printData(evt.target);
    })
  },
  
  printData(el) {
    console.log("clicked!", el.innerText);
  }
}

myObj.register();
```





