## JavaScript로 DOM을 렌더링하기
Javascript로 DOM 화면을 렌더링하기 위해 관련 메서드를 찾다가 유사하면서도 다른 여러 메서드들을 알게 됐다. Element.innerHTML, Element.insertAdjacentHTML, Node.appendChild 등 관련 메서드가 있는데, 메서드를 살펴보기 전에 Element와 Node가 무엇인지부터 체크하자.

## EventTarget vs Element vs Node
![](https://images.velog.io/images/jangws/post/d89ef85f-88d4-46e0-bea9-20ef01c62ff2/eventTargetTree.png)

### EventTarget
- EventTarget 인터페이스는 이벤트를 수신할 수 있고, 수신한 이벤트에 대한 수신기(listener)를 가질 수 있는 객체가 구현하는 인터페이스이다.
- EventTarget의 자식으로 Node나 Window가 있다.
- 주요 메서드로는 `EventTarget.addEventListener()`, `EventTarget.removeEventListener()`, `EventTarget.dispatchEvent()` 등이 있다.

### Node
- Node는 부모인 EventTarget으로부터 속성을 상속받았다.
- Node는 여러 가지 DOM 타입들(Document, Element, CharacterData, DocumentFragment, DocumentType)의 부모로서, 여러 DOM 타입들은 Node로부터 속성을 상속받아 비슷하게 처리될 수 있다.
- Node는 속성이나 메소드가 적합하지 않은 경우에 null을 반환할 수 있다.
- 주요 속성으로는 `Node.childNodes`, `Node.parentNode`, `Node.firstChild`, `Node.lastChild`, `Node.nextSibling`, `Node.previousSibling`, `Node.textContent`이 있다.
- 주요 메소드로는 `Node.appendChild()`, `Node.cloneNode()`, `Node.hasChildNodes()`, `Node.insertBefore()`, `Node.removeChild()`, `Node.replaceChild()`
> 참고로 DOM(문서 개체 모델, Document Object Model)은 자바스크립트 Node 개체의 계층화된 트리다.

### Element
- Element 예시 : `<body>`, `<a>`, `<p>` 등과 같은 노드 
> 참고로 Element 노드는 아니지만 Node 중에 `window.document` 등과 같은 Document 노드, 줄바꿈과 공백을 포함한 텍스트인 Text 노드, `class="cool"`과 같은 Attribute 노드 등도 있다)
- Node와 EventTarget은 Element의 부모이므로, Element는 Node와 EventTarget의 속성을 상속한다.  
- Element는 Document 안의 모든 객체가 상속하는 제일 범용적인 클래스로서 공통 메서드와 속성만 갖고 있다. Element의 속성을 상속받은 [HTMLElement](https://developer.mozilla.org/ko/docs/Web/API/HTMLElement)나 [SVGElement](https://developer.mozilla.org/en-US/docs/Web/API/SVGElement)도 있다. 
- 주요 속성으로는 `Element.classList`, `Element.id` `Element.innerHTML`, `Element.outerHTML` 등이 있다.
- 주요 메서드로는 `EventTarget.addEventListener()`, `Element.insertAdjacentElement()`, `Element.insertAdjacentHTML()`, `Element.querySelector()`, `Element.remove()` 등이 있다.

## Element.innerHTML
- innerHTML은 Element의 **속성**이며, Element 내에 포함된 HTML(또는 XML) 마크업을 가져오거나 설정한다.
- 구문
```jsx
const content = element.innerHTML;

element.innerHTML = htmlString;
```
- 값은 `DOMString`이다. 
- innerHTML 값을 설정할 때, 다음 과정을 거쳐서 작동한다.
> 1. 지정한 값은 HTML 또는 XML(문서 타입에 따라)로 파싱되어, DocumentFragment 객체가 새 요소에 대한 새로운 노드 DOM 노드 집합을 나타냅니다. 
> 2. 내용이 대체되는 요소가 `<template>` 요소 인 경우, `<template>` 요소의 content (en-US) 속성(attribute)은 1단계에서 작성한 새  DocumentFragment 로 대체됩니다.
> 3. 다른 모든 요소의 경우, 요소의 내용은 새 DocumentFragment 의 노드로 대체됩니다.
### [보안 고려사항](https://developer.mozilla.org/ko/docs/Web/API/Element/innerHTML#security_considerations)
- innerHTML를 사용하여 웹페이지에 텍스트를 삽입한 경우, 사이트의 공격 경로가 되어 잠재적인 보안 위험이 발생할 수도 있다고 한다. 
- 따라서 일반 텍스트를 삽입 할 때는 innerHTML을 사용하지 않는 것이 좋고, 대신에  `Node.textContent`를 사용하라고 MDN은 권장한다.`Node.textContent`는 전달된 내용을 HTML로 파싱하지 않고 원시 텍스트(raw text)로 삽입하기 때문에 안전하다.
- 또한, DOM에 삽입 전에 위험성을 확인할 수 있는 패키지([DomPurify](https://github.com/cure53/DOMPurify)) 등을 활용할 수도 있다.

## Element.insertAdjacentHTML()
- insertAdjacentHTML() 메서드는 HTML이나 XML 같은 텍스트를 파싱하고, 특정 위치에 DOM tree 안에 원하는 node들을 추가한다. innerHTML 등의 메서드들보다 삽입하려는 위치를 더 세밀하게 다룰 수 있다.
- 이미 사용중인 element는 다시 파싱하지 않는다. 그러므로 element 안에 존재하는 element를 건드리지 않는다. innerHtml보다 작업이 덜 드므로 더 빠르다.
- 구문
```jsx
element.insertAdjacentHTML(position, text);
// postion에는 beforebegin, afterbegin, beforeend, afterend가 있다.
// text(인자)는 HTML 또는 XML로 해석될 수 있는 문자열이다.
```

```
// position의 예시
<!-- [beforebegin] : element 앞에 --> 
<p>
<!-- [afterbegin] : element 안에 가장 첫번째 child -->
foo
<!-- [beforeend] : element 안에 가장 마지막 child -->
</p>
<!-- [afterend] : element 뒤에 -->
```

## Node.appendChild()
-  appendChild() 메서드는 한 노드 개체를 DOM 트리인 특정 부모 노드의 자식 노드 리스트 중 마지막 자식으로 붙인다.
- 만약 인자로 주어진 노드가 이미 문서에 존재하는 노드를 참조하고 있다면 appendChild() 메소드는 해당 노드를 현재 위치에서 새로운 위치로 이동시킨다.(만약 인자로 주어진 노드가 이미 부모를 가지고 있다면 우선 그곳에서 삭제되고 새로운 위치로 이동된다. 따라서 문서에 존재하는 노드를 다른 곳으로 붙이기 전에 부모 노드로부터 지워버릴 필요가 없다.)
- [참고] 즉, 한 노드는 문서상의 두 지점에 동시에 존재할 수 없다. 
- appendChild()와 비슷한 메서드로서 Node.insertBefore()가 있다. Node.insertBefore(삽입될 노드, 삽입될 노드가 앞으로 올 참조 노드) 메서드는 두 번째 매개변수가 전달되지 않을 경우, appendChild()처럼 동작한다.

- 구문
```jsx
element.appendChild(node);
// 인자로 넣을 node로는 document.createElement(tagName)로 새로 만들어서 사용하거나, 이미 문서에 존재하는 노드를 참조할 수도 있다.
```


## innerHTML, innerAdjacentHTML, appendChild 성능 비교
- innerHTML이 비교적 느리고, insertAdjacentHTML이 비교적 빠른 편이다.
- innerHTML은 무겁고 비싼 대가를 치르는 HTML 파서를 호출하기 때문에, 만약 텍스트 노드 정도 삽입하는 경우에는 textContent를 사용하는 것이 낫다.

![](https://images.velog.io/images/jangws/post/f8b02523-fe9f-48c5-b025-3af0c28c6cf0/innerHTML%20benchmark.jpg)


> ### Reference
https://developer.mozilla.org/
https://www.measurethat.net/Benchmarks/Show/16493/1/innerhtml-vs-insertadjacenthtml-vs-appendchild-vs-inser



