책 : 모던 자바스크립트 Deep Dive(이웅모)

# 자바스크립트 기본 개념
- ES6(ECMAScript 2015) : let/const, 클래스, 화살표 함수, 템플릿 리터럴, 디스트럭처링 할당, 스프레드 문법, rest 파라미터, 심벌, 프로미스, Map/Set, 이터러블, for...of, 제너레이터, Proxy, 모듈 import/export
- Ajax : 1999년, 자바스크립트를 이용해 서버와 브라우저가 비동기 방식으로 데이터를 교환할 수 있는 통신 기능이다. Asynchronous JavaScript and XML, 웹페이지에서 변경할 필요가 없는 부분은 다시 렌더링하지 않고, 서버로부터 필요한 데이터만 전송받아 변경해야 하는 부분만 한정적으로 렌더링하는 방식이 가능해졌다. 
- Node.js : 2009년, Ryan Dahl이 발표한 Node.js는 구글 V8 자바스크립트 엔진으로 빌드된 자바스크립트 런타임 환경이다. Node.js는 브라우저의 자바스크립트 엔진에서만 동작하던 자바스크립트를 브라우저 이외의 환경에서도 동작할 수 있도록 자바스크립트 엔진을 브라우저에서 독립시킨 자바스크립트 실행 환경이다. 주로 서버 사이드 애플리케이션 개발에 사용되며, 이에 필요한 모듈, 파일시스템, HTTP 등 빌트인 API를 제공한다.
  * Node.js는 데이터를 실시간으로 처리하기 위해 I/O가 빈번하게 발생하는 SPA(Single Page Application)에 적합하다. 하지만 CPU 사용률이 높은 애플리케이션에는 권장되지 않는다.
  * Node.js는 클라이언트 사이드 Web API를 지원하지 않고 ECMAScript와 Node.js 고유의 API를 지원한다.
  * npm : npm(node package manage)은 자바스크립트 패키지 매니저다. Node.js에서 사용할 수 있는 모듈
  > SPA란 : 어떤 웹 사이트의 전체 페이지를 하나의 페이지에 담아 동적으로 화면을 바꿔가며 표현하는 것이 SPA이다. 뭔가를 클릭하거나 스크롤하면, 상호작용하기 위한 최소한의 요소만 변경이 일어난다. 페이지 변경이 일어난다고 보여지는 것 또한 최초 로드된 자바스크립트를 통해 미리 브라우저에 올라간 템플릿만 교체되는 것이다.
- SPA 프레임워크 : CBD(Component based development) 방법론을 기반으로 하는 SPA가 대중화되면서 Angular, React, Vue.js, Svelte 등 다양한 SPA프레임워크/라이브러리가 사용되고 있다.
- ECMAScript : 자바스크립트의 표준 사양인 ECMA-262를 말하며, 프로그래밍 언어의 값, 타입, 객체와 프로퍼티, 함수, 표준 빌트인 객체 등 핵심 문법을 규정한다. 각 브라우저 제조사는 ECMAScript 사양을 준수해서 브라우저에 내장되는 자바스크립트 엔진을 구현한다. 
  * 자바스크립트는 일반적으로 ECMAScript를 기본 뼈대로 갖는 개념이며, 브라우저가 별도 지원하는 클라이언트 사이드 Web API를 아우르는 개념이다. Web API는 ECMAScript와 별도로 W3C에서 별도의 사양으로 관리하고 있다(https://developer.mozilla.org/ko/docs/Web/API).
- 자바스크립트는 명령형, 함수형, 프로토타입 기반 객체지향 프로그래밍을 지원하는 멀티 패러다임 프로그래밍 언어다.(클래스 기반 객체지향 언어보다 효율적이면서 강력한 프로토타입 기반의 객체지향 언어다).

## 변수
- 메모리는 데이터를 저장할 수 있는 메모리 셀의 집합체다. 메모리 셀 하나의 크기는 1바이트(8비트)이며, 컴퓨터는 메모리 셀의 크기, 즉 1바이트 단위로 데이터를 저장하거나 읽어들인다. 각 셀은 고유의 메모리 주소(memory address)를 갖는다.
- 변수(variable) : 변수는 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름을 말한다. 즉, 변수는 값의 위치를 가리키는 상징적인 이름이다. 
  * 메모리 공간에 저장된 값을 식별할 수 있는 고유한 이름을 변수 이름이라고 하고, 변수에 저장된 값을 변수 값이라고 한다. 변수에 값을 저장하는 것을 할당(assignment)이라 하고, 변수에 저장된 값을 읽어들이는 것을 참조(reference)라 한다. 
  * 식별자(identifier) : 변수 이름을 식별자라고도 한다(변수, 함수, 클래스 등의 이름은 모두 식별자다). 식별자는 어떤 값을 구별해서 식별할 수 있는 고유한 이름을 말한다. 식별자는 값이 아니라 메모리 주소를 기억하고 있다. 즉, 식별자는 메모리 주소에 붙인 이름이라고 할 수 있따. 
- 변수를 사용할 때는 반드시 선언이 필요하다. 변수 선언은 선언 단계(변수 이름 등록)와 초기화 단계(메모리 공간 확보하고 undefined 할당)를 거친다.
  * var 키워드는 블록레벨 스코프를 지원하지 않아, 의도하지 않게 전역 변수가 선언되어 심각한 부작용이 발생하기도 한다.
- 변수 이름 등 모든 식별자는 실행 컨텍스트에 등록된다. 변수 이름과 변수 값은 실행 컨텍스트 내에 Key / Value 형식인 객체로 등록되어 관리된다. 
> 실행 컨텍스트(execution context)는 자바스크립트 엔진이 소스코드를 평가하고 실행하기 위해 필요한 환경을 제공하고 코드의 실행 결과를 실제로 관리하는 영역이다. 자바스크립트 엔진은 실행 컨텍스트를 통해 식별자와 스코프를 관리한다.

- 변수 호이스팅(variable hoisitng) : 변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 변수 호이스팅이라 한다. 자바스크립트 엔진은 변수 선언이 소스코드의 어디에 있든 상관없이 다른 코드보다 먼저 실행한다. 따라서 변수 선언이 소스코드의 어디에 위치하는지와 상관없이 어디서든지 변수를 참조할 수 있다. 변수 선언뿐 아니라 var, elt, const, functino, class 키워드를 사용해서 선언하는 모든 식별자는 호이스팅된다. 
- 변수 재할당 : 변수에 값을 재할당하면 변수의 값은 이전 값에서 재할당한 값으로 변경된다. 처음 값을 할당했을 때와 마찬가지로 이전 값이 저장되어 있던 메모리 공간을 지우고 그 메모리 공간에 재할당 값을 새롭게 저장하는 것이 아니라 새 메모리 공간을 확보하고 그 메모리 공간에 새 변수 값을 저장한다. 
- Garbage Collecotr : 가비지 콜렉터는 애플리케이션이 할당(allocate)한 메모리 공간을 주기적으로 검사하여 더 이상 사용되지 않는 메모리를 해제(release)하는 기능을 말한다. 더 이상 사용되지 않는 메모리란 간단히 말하자면 어떤 식별자도 참조하지 않는 메모리 공간을 의미한다. 자바스크립트는 가비지 콜렉터를 내장하고 있는 managed language(개발자가 직접적으로 메모리 제어 불가)로서 가비지 콜렉터를 통해 메모리 누수를 방지한다.
- 식별자 네이밍 규칙 : 자바스크립트에서는 일반적으로 변수나 함수의 이름에는 카멜 케이스(firstName)를 사용하고, 생성자 함수, 클래스 이름에는 파스칼 케이스(FirstName)을 사용한다. 


## 표현식과 문
- 값(value) : 값은 식(expression)이 평가(evaluate, 식을 해석해서 값 생성 또는 참조)되어 생성된 결과를 말한다. 모든 값은 데이터 타입을 가지며, 메모리에 2진수(bit)의 나열로 저장된다.
- 리터럴(literal) : 리터럴은 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용해 값을 생성하는 표기법을 말한다. 
- 표현식(expression) : 값으로 평가될 수 있는 문(statement)은 모두 표현식이다.
- 문(statement) : 문은 프로그램을 구성하는 기본 단위이자 최소 실행 단위다. 문의 집합으로 이뤄진 것이 바로 프로그램이다.(var = sum 1 + 2;) 
  * 표현식인 문 : 값으로 평가되므로 변수에 할당할 수 있다.(ex, x=100; //할당문은 그 자체가 표현식이지만 완전한 문이기도 하다.)
  * 표현식이 아닌 문 : 값으로 평가할 수 없으므로 변수에 할당하면 에러가 난다.(ex, var x; //변수 선언문은 표현식이 아닌 문이다.)
- 토큰(token) : 문은 여러 토큰으로 구성된다. 토큰이란 문법적인 의미를 가지며, 문법적으로 더 이상 나눌 수 없는 코드의 기본 요소를 의미한다.(var, sum, =, 1, +, 2, ;) 


## 데이터 타입
- 자바스크립트(ES6)는 7개의 데이터 타입을 제공한다.
  - 원시 타입
    1. 숫자 타입 : 자바스크립트에서 숫자 타입은 모두 실수로만 처리된다. 숫자 타입은 추가적으로 세 가지 특별한 값(Infinity, -Infinity, NaN)도 표현할 수 있다.
    2. 문자열 타입 : 템플릿 리터럴(백틱 사용)은 멀티라인 문자열과 표현식 삽입을 가능하게 한다. (ex, console.log(\`1 + 2 = %{1 + 2}.\`);)
    3. 불리언 타입 : true, false
    4. undefined 타입 : 변수 선언한 이후 값을 할당하지 않은 변수를 참조하면 undefined가 반환된다. undefined는 개발자가 아니라 자바스크립트 엔진이 변수를 초기화할 때 사용하는 타입이다.  
    5. null 타입 : 개발자가 변수에 값이 없다는 것을 의도적으로 명시하고 싶을 때는 undefined가 아니라 null을 사용한다. 
    6. symbol 타입 (ES6에서 추가된 7번째 타입) : 심벌 값은 다른 값과 중복되지 않는 유일무이한 값이다. 주로 이름이 충돌할 위험이 없는 객체의 유일한 프로퍼티 키를 만들기 위해 사용한다. Symbol 함수를 호출해 생성한다. 
        ```js
        var key = Symbol('key');
        var obj = {}
        //이름이 충돌할 위험이 없는 유일무이한 값인 심벌을 프로퍼티 키로 사용한다.
        obj[key] = 'value';
        console.log(obj[key]); //value
        ```
  - 객체 타입(객체, 함수, 배열 등)

- 데이터 타입이 필요한 이유
  * 값을 저장할 때 확보해야 하는 메모리 공간의 크기를 결정하기 위해
  * 값을 참조할 때 한 번에 읽어 들여야 할 메모리 공간의 크기를 결정하기 위해
  * 메모리에서 읽어 들인 2진수를 어떻게 해석할지 결정하기 위해

- 동적 타이핑
  * 자바스크립트는 동적 타입 언어로서 변수를 선언할 때 타입을 선언하지 않는다. 다만 var, let, const 키워드를 사용해 변수를 선언할 뿐이다. 자바스크립트의 변수는 정적 타입 언어와 같이 미리 선언한 데이터 타입의 값만 할당할 수 있는 것이 아니다. 어떠한 데이터 타입의 값이라도 자유롭게 할당할 수 있다.
  * 자바스크립트의 변수는 선언이 아닌 할당에 의해 타입이 결정(타입 추론 type inference)된다. 재할당에 의해 변수의 타입은 언제든지 동적으로 변할 수 있다. 이러한 특징을 동적 타이핑이라 한다. 대표적 동적 타입 언어로는 자바스크립트, 파이썬, 루비 등이 있다.
  * 변수는 타입을 갖지 않고 값이 타입을 가지므로 현재 변수에 할당되어 있는 값에 의해 타입이 동적으로 결정된다.(변수는 값에 묶여 있는 값에 대한 별명이다)
  * 동적 타입 언어는 유연성은 높지만 신뢰성은 떨어진다. (개발자 의도와 상관없이 타입이 자동으로 변환될 수도 있기 때문)

## 연산자
연산자(operator)는 하나 이상의 표현식을 대상으로 산술, 할당, 비교, 논리, 타입, 지수 연산 등을 수행해 하나의 값을 만든다. 이때 연산의 대상을 피연산자(operand)라 한다. 피연산자는 값으로 평가될 수 있는 표현식이어야 한다. 
- 증가/감소(++/--)연산자는 피연산자의 값을 변경하는 부수 효과가 있으며, 위치에 의미가 있다.
  * 피연산자 앞에 위치한 전위 증가/감소 연산자는 먼저 피연자의 값을 증가/감소시킨 후, 다른 연산을 수행한다.
    ```js
    var x = 5, result;
    result = ++x;
    console.log(result, x); //6 6
    ```
  * 피연산자 뒤에 위치한 후위 증가/감소 연산자는 먼저 다른 연산을 수행한 후, 피연산자의 값을 증가/감소시킨다.
    ```js
    var x = 5, result;
    result = x++; //x의 값(5)을 result에 할당한 다음, x의 값을 증가(6)시킨다. 
    console.log(result, x); //5 6
    ```
- 비교 연산자
  * 동등 비교 연산자(==, !=)는 느슨한 비교(값만 비교)를 하지만 일치 비교 연산자(===, !==)는 엄격한 비교(값과 타입 모두 비교)를 한다.
    ```js
    // 타입은 다르지만 암묵적 타입 변환을 통해 타입을 일치시키면 동등하다. 
    5 == '5'; // true
    ```
    + 동등 비교 연산자는 예측하기 어렵고 실수할 수 있어 사용하지 않는 편이 좋고, 대신 일치 비교 연산자를 사용한다.
    + 일치 비교 연산자에서 주의할 것은 NaN이다. NaN은 자신과 일치하지 않는 유일한 값이다. 따라서 숫자가 NaN인지 조사하려면 빌트인 함수 isNaN을 사용한다.
      ```js
      NaN === NaN; // false
      isNaN(NaN); // true
      ```
    + Object.is 메서드 : ES6에서 도입된 이 메서드는 다음과 같이 예측 가능한 정확한 비교 결과를 반환한다.
      ```js
      -0 === +0; //true
      Object.is(-0, +0); //false
      NaN === NaN; //false
      Object.is(NaN, NaN); true
      ```
- 삼항 조건 연산자(ternary operator) : 조건식의 평가 결과에 따라 반환할 값을 사용한다. 물음표 앞의 첫 번째 피연산자는 조건식, 즉 불리언 타입의 값으로 평가될 표현식이고, 조건식이 참이면 콜론 앞의 두 번째 피연산자가 평가되어 반환되고, 거짓이면 콜론 뒤의 세 번째 피연산자가 평가되어 반환된다. 삼항 조건 연산자 표현식은 값으로 평가할 수 있는 표현식인 문이다. 
  ```js
  var result = score >= 60 ? 'pass' : 'fail';
- 논리 연산자(logical operator)
  * || : 논리합(OR)
  * && : 논리곱(AND)
  * ! : 부정(NOT), 논리부정 연산자는 언제나 불리언 값을 반환한다. 만약 피연사자가 불리언 값이 아니면 불리언 타입으로 암묵적 타입 변환된다. 
- typeof 연산자 : 피연산자의 데이터 타입을 7가지 문자열(string, number, boolean, undefined, symbol, object, function) 중 하나로 반환한다. 이처럼 typeof 연산자가 반환하는 문자열은 7개의 데이터 타입과 정확히 일치하지는 않는다
  * null의 타입은 object로 반환됨에 주의하자. 값이 null 타입인지 확인할 때는 typeof 연산자를 사용하지 말고 일치 연산자(===)를 사용하자.
  ```js
  var foo = null;
  typeof foo === null; // false
  foo === null; // true
  ```
- delete 연산자 : 객체의 프로퍼티를 삭제한느 부수 효과가 있다. 
 ```js
 var o = { a : 1 };
 delete o.a;
 console.log(o); //{}
 ```
 
## 제어문
- 블록문 : 문을 중괄호로 묶은 것이다. 블록문은 언제나 문의 종료를 의미하는 자체 종결성을 갖기 때문에 블록문의 끝에는 세미콜론을 붙이지 않는다.
- 조건문
  * if...else 문
  ```js
  if (조건식1) {
  } else if (조건식2) {
  } else {
  }
  ```
  삼항 조건 연산자로 바꿔 쓸 수 있다. 경우의 수가 세 가지 다음과 같이 바꿔 쓸 수도 있다.
  ```js
  //0은 false로 취급된다
  var kind = num ? (num>0 ? '양수' : '음수') : '영'; 
  ```
  * switch문 : 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case 문으로 실행 흐름을 옮긴다. 
  ```js
  switch (표현식) {
    case 표현식1:
      //switch 문의 표현식과 표현식1이 일치되면 실행될 문;
      break;  // fall through가 나타지 않도록 break 문을 사용해야 한다.
    case 표현식2:
      //switch 문의 표현식과 표현식2가 일치되면 실행될 문;
      break;
    default:
      //switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문;
  }
  ```
- 반복문
  * 1. for 문 : 반복 횟수가 명확할 때 주로 사용한다.
  ```js
  for (변수 선언문 또는 할당문; 조건식; 증감식) {
    조건식이 참인 경우 반복 실행될 문;
  }
  ```
  * 2. while 문 : 반복 횟수가 불명확할 때 주로 사용한다.
  ```js
  var count = 0;
  while (true) {
    console.log(count);
    count++;
    if (count === 3) break;  //무한루프 탈출하려면 코드 블록 내에 if 문으로 조건을 만들고 break 문으로 코드 블록 탈출
  }
  ```
  * 3. do...while 문 : 코드 블록을 먼저 실행하고 조건식을 평가한다. 따라서 코드 블록은 무조건 한 번 이상 실행된다. 
  ```js
  var count = 0;
  do {
    console.log(count); // 0 1 2
    count++;
  } while(count <3);
  ```
  * 반복문을 대체할 수 있는 다양한 기능 : 배열을 순회할 때 사용하는 forEach메서드, 객체의 프로퍼티를 열거할 때 사용하는 for...in 문, ES^에서 도입된 이터러블을 순회할 수있는 for...of 문과 같이 반복문을 대체할 수 있는 기능들도 있다.

- break 문 : label 문, 반복문, switch 문의 코드 블록 외에 break 문을 사용하면 SyntaxError가 발생한다. 
  * label 문 : 식별자가 붙은 문이며, 프로그램의 실행 순서를 제어하는 데 사용한다. 
  ```js
  //foo라는 식별자가 붙은 레이블 블록문
  foo: {
    console.log(1);
    break foo; //foo 레이블 블록문을 탈출한다.
    console.log(2);
  }
  console.log('Done!');
  ```
- continue 문 : 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다. break 문처럼 반복문을 탈출하지는 않는다.  

## 타입 변환과 단축 평가
- 논리 연산자를 사용한 단축평가 : 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환한다. 이를 단축평가라 한다. 단축평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것을 말한다.
true || anything   ->   true
  * false || anything   ->  anything
  * true && anything   ->   anything
  * false && anything   ->  false
   ```js
   console.log(
  'Cat' || 'Dog',  //Cat
  false || 'Dog',  //Dog
  'Cat' || false,  //Cat
  'Cat' && 'Dog',  //Dog
  false && 'Dog',  //false
  'Cat' && false)  //false
  ```
- 객체는 key와 value로 구성된 프로퍼티의 집합이다. 만약 객체를 가리키기를 기대하는 변수의 값이 객체가 아니라 null 또는 undefined인 경우 객체의 프로퍼티를 참조하면 타입 에러가 발생하고 프로그램이 강제 종료된다. 이때 단축 평가를 발생하면 에러를 발생시키지 않는다.
  ```js
  var elem = null;
  var value = elem && elem.value; // -> null
  ```
  * 옵셔널 체이닝 연산자 : ES11에 도입된 옵셔널 체이닝 연산자 ?.는 좌항의 연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다. 옵셔널 체이닝 연산자 ?.는 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때 유용하다. 옵셔널 체이닝 연산자 ?.가 도입되기 이전에는 논리 연산자 &&를 사용한 단축 평가를 통해 변수가 null 또는 undefined인지 확인했다.
   ```js
   var value = elem?.value;
   ```
  * null 병합 연산자 : ES11에서 도입된 null 병합 연산자 ??는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다. null 병합 연산자 ??는 변수에 기본값을 설정할 때 유용하다. null 병합 연산자 ??가 도입되기 이전에는 논리 연산자 ||를 사용한 단축 평가를 통해 변수에 기본값을 설정했다. 
 ```js
 var foo = null ?? 'default string';
 console.log(foo); // "default string"
 ```
- 함수를 호출할 때 인수를 전달하지 않으면 매개변수에는 undefined가 할당된다. 이때 단축 평가를 사용해 매개변수의 기본값을 설정하면 undefined로 인해 발생할 수 있는 에러를 방지할 수 있다.

## 객체 리터럴
- 객체(object) : 자바스크립트는 객체 기반의 프로그래밍 언어이며, 자바스크립트를 구성하는 거의 '모든 것'이 객체다. 원시 값을 제외한 나머지 값(함수, 배열, 정규 표현식 등) 모두 객체다.원시 값은 단 하나의 값을 나타내며 변경 불가능한 값이지만, 객체는 복합적인 자료구조며 변경 가능한 값이다. 객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 key와 value로 구성된다.
  * 함수도 객체의 프로퍼티 값으로 사용될 수 있으며, 이처럼 프로퍼티 값으로 사용된 함수는 일반 함수와 구분하기 위해 method라 부른다. 즉 객체는 프로퍼티와 메서드로 구성된 집합체다.
    + 프로퍼티 : 객체의 상태를 나타내는 값(data)
    + 메서드 : 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작(behavior)
![다운로드](https://user-images.githubusercontent.com/59413128/135813148-4ab11911-7722-40fa-93e3-19c212b26178.png)

- 자바스크립트는 '프로토타입 기반 객체지향 언어'로서 '클래스 기반 객체지향 언어(C++,자바)'와는 달리 다양한 객체 생성 방법을 지원한다. 
  * 객체 리터럴, Object 생성자 함수, 생성자 함수, Object.create 메서드, 클래스(ES6)
 > C++나 자바 같은 클래스 기반 객체지향 언어는 클래스를 사전에 정의하고 필요한 시점에 new 연산자와 함께 생성자(constructor)를 호출하여 인스턴스를 생성하는 방식으로 객체를 생성한다.
 > > 인스턴스란 클래스에 의해 생성되어 메모리에 저장된 실체를 말한다. 객체지향 프로그래밍에서는 객체는 클래스와 인스턴스를 포함한 개념이다. 클래스는 인스턴스를 생성하기 위한 템플릿의 역할을 한다. 인스턴스는 객체가 메모리에 저장되어 실제로 존재하는 것에 초점을 맞춘 용어다.
- 객체 리터럴에 의한 객체 생성(가장 일반적이며 간단한 방법)
  * 객체 리터럴은 중괄호 내에 0개 이상의 프로퍼티를 정의한다. 
  ```js
  var person = {
    name: 'Lee',
    sayHello: function() {
      console.log('Hello! My name is %{this.name}');
    }
  };
  console.log(typeof person); //object
  console.log(person); // {name: "Lee", sayHello: f}
  ```
  
- 프로퍼티 : 객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다. 프로퍼티를 나열할 때는 쉼표로 구분한다.
  * 문자열 또는 문자열로 평가할 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다 .이 경우에는 프로퍼티 키로 사용할 표현식을 대괄호로 묶어야 한다. 
  ```js
  var obj = {};
  var key = 'hello';
  obj[key] = 'world';
  //var obj = { [key]: 'world};
  console.log(obj); // {hello: "world"}
  ```
  
- 프로퍼티 접근
  * 마침표 표기법
  ```js
  var person = {
    name: 'Lee'
  };
  console.log(person.name);  //Lee
  ```
  * 대괄호 표기법 : 대괄호 표기법을 사용하는 경우 대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야 한다.
  ```js
  console.log(person['name']; //Lee
  ```
- 프로퍼티 삭제 : delete 연산자
```js
var person = {
  name: 'Lee'
};
delete person.name;
```

- ES6에 추가된 객체 리터럴의 확장 기능
  * 프로퍼티 축약 표현 : 프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일 때 프로퍼티 키를 생략할 수 있다. 이때 프로퍼티 키는 변수 이름으로 자동 생성된다.
  ```js
  let x=1, y=2;
  const obj = {x,y};  //이전에는  var obj = {x: x, y: y}라고 했어야 했다.
  ``` 
  * 계산된 프로퍼티 이름 : 문자열 또는 문자열로 타입 변환할 수 있는 값으로 평가되는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다. 단, 프로퍼티 키로 사용할 표현식을 대괄호로 묶어야 한다.
  ```js
  const prefix = 'prop';
  let i =0;
  //객체 리터럴 내부에서 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성
  const obj = {
    [`${prefix}-${++i}`]: i,
    [`${prefix}-${++i}`]: i,
    [`${prefix}-${++i}`]: i
  }
  console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
  ```
  * 메서드 축약 표현 : ES5에서 메서드를 정의하려면 프로퍼티 값으로 함수를 할당했으나, ES6에서는 메서드를 정의할 때 function 키워드를 생략한 축약 표현을 사용할 수 있다.
  ```js
  const ojb = {
    name: 'Lee',
    sayHi() {    //이전에는 sayHi: function()였음
      console.log('Hi!'+name);
    }
  };
  obj.sayHi(); //Hi! Lee
  ```
## 원시 값과 객체의 비교
- 원시 타입의 값
  1. 변경 불가능하다.
  2. 변수에 할당하면 변수(확보된 메모리 공간)에는 실제 값이 저장된다.
  3. 원시 값을 갖는 변수를 다른 변수에 할당하면 원본의 원시 값이 복사되어 전달된다. 이를 값에 의한 전달(pass by value)이라 한다.
- 객체(참조) 타입의 값
  1. 변경 가능하다.
  2. 변수에 할당하면 변수(확보된 메모리 공간)에는 참조 값이 저장된다.
  3. 객체를 가리키는 변수를 다른 변수에 할당하면 원본의 참조 값이 복사되어 전달된다. 이를 참조에 의한 전달(pass by reference)이라 한다.

- 유사 배열 객체(array-like object) : 유사 배열 객체란 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고 length 프로퍼티를 갖는 객체를 말한다. 문자열은 마치 배열처럼 인덱스를 통해 각 문자에 접근할 수 있으며, length프로퍼티를 갖기 때문에 유사 배열 객체이고 for 문으로 순회할 수도 있다. 이치럼 원시 값인 문자열이 객체이기도 하다. 하지만 문자열은 원시 값이므로 값을 변경할 수 없다.
- 객체의 참조에 의한 전달 : 객체를 가리키는 변수를 다른 변수에 할당하면 원본의 참조 값이 복사되어 전달된다. 이것은 두 개의 식별자가 하나의 객체를 공유한다는 것을 의미한다. 원본 또는 사본 중 어느 한쪽에서 객체를 변경(변수에 새로운 객체를 재할당하는 것이 아니라 객체의 프로퍼티 값을 변경하거나 프로퍼티를 추가, 삭제)하면 서로 영향을 주고받는다.

## 함수
- 프로그래밍 언어의 함수는 일련의 과정을 문(statement)으로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것이다. 함수 내부로 입력을 전달받는 변수를 매개변수(parameter), 입력을 인수(argument), 출력을 반환값(return value)이라 한다. 함수는 몇 번이든 호출할 수 있으므로 코드의 재사용이라는 측면에서 매우 유용하다. 코드의 중복을 억제하고 재사용성을 높이는 함수는 유지보수의 편의성을 높이고 실수를 줄여 코드의 신뢰성을 높인다. 
- 함수 리터럴 : 리터럴은 값을 생성하기 위한 표기법이며, 함수 리터럴도 평가되어 값을 생성한다. 즉, 함수는 객체다. 함수는 객체지만 일반 객체와 달리, 호출을 할 수 있으며 고유한 프로퍼티를 갖는다. 함수가 객체라는 사실은 다른 프로그래밍 언어와 구별되는 자바스크립트의 중요한 특징이다. 
  ```js
  // 변수에 함수 리터럴을 할당
  var f = function add(x,y) {
    return x+y;
  };
  ```
- 함수 정의 방식
  * 함수 선언문 : 함수 선언문은 함수 이름을 생략할 수 없다는 점을 제외하면 함수 리터럴과 형태가 동일하다. 함수 선언문은 표현식이 아닌 문이다.
    > 표현식이 아닌 문 : 값으로 평가할 수 없으므로 변수에 할당하면 에러가 난다.(ex, var x; //변수 선언문은 표현식이 아닌 문이다.) 
    ```js
    function add(x,y) {
      return x + y;
    }
  * 함수 표현식 : 자바스크립트의 함수는 입급 객체며, 이는 함수를 값처럼 자유롭게 사용할 수 있다는 의미다. 함수는 일급 객체이므로 함수 리터럴로 생성한 함수 객체를 변수에 할당할 수 있다. 함수 리터럴의 함수 이름은 생략할 수 있다. 이러한 함수를 익명 함수라 한다. 함수 표현식의 함수 리터럴은 함수 이름을 생략하는 것이 일반적이다. 함수를 호출할 때는 함수 이름이 아니라 함수 객체를 가리키는 식별자를 사용해야 한다. 
    > 표현식인 문 : 값으로 평가되므로 변수에 할당할 수 있다.(ex, x=100; //할당문은 그 자체가 표현식이지만 완전한 문이기도 하다.)
   ```js
   var add = function foo (x, y) {  //함수 이름 foo 생략 가능
     return x + y; 
   };
   
   console.log(add(2,5)); 
   ```
  * 함수 생성 시점과 함수 호이스팅
    + 함수 선언문으로 정의한 함수는 함수 선언문 이전에 호출할 수 있다. 이는 함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수의 생성 시점이 다르기 때문이다. 함수 선언문으로 함수를 정의하면 런타임 이전에 함수 객체가 먼저 생성된다. 자바스크립트 엔진은 함수 이름과 동일한 이름의 식별자를 암묵적으로 생성하고 생성된 함수 객체를 할당한다. 이처럼 함수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 함수 호이스팅이라 한다. 
      ```js
      console.dir(add); // f add(x,y)
      console.log(add(2,5); // 7
      
      function add(x, y) {
        return x + y;
      }
      ```
    + 그러나 함수 표현식으로 정의한 함수는 함수 표현식 이전에 호출할 수 없다. 함수 표현식으로 함수를 정의하면 함수 호이스팅이 발생하는 것이 아니라 변수 호이스팅이 발생한다. g 따라서 함수 표현식으로 정의한 함수는 반드시 함수 표현식 이후에 참조 또는 호출해야 한다. 
      ```js
      console.dir(sub); // undefined
      console.log(sub(2,5)); // TypeError : sub is not a function
      
      var sub = function (x, y) {
        return x - y;
      }
      ```
     >  함수 호이스팅은 함수를 호출하기 전에 반드시 함수를 선언해야 한다는 당연한 규칙을 무시한다. 이 같은 문제 때문에 함수 선언문 대신 함수 표현식 사용이 권장되기도 한다.
  * Function 생성자 함수 : 빌트인 함수인 Function 생성자 함수에 매개변수 목록과 함수 몸체를 문자열에 전달하면서 new 연산자와 함께 호출하면 함수 객체를 생성해서 반환한다. 사실 new 연산자 없이 호출하면 결과는 동일하다. 이 방식은 일반적이지 않으며 바람직하지도 않다. 클로저를 생성하지 않는 등, 다른 함수 생성 방식과 다르게 동작한다.
     > 생성자 함수(constructor function)는 객체를 생성하는 함수를 말한다. 객체를 생성하는 방식은 객체 리터럴 이외에 다양한 방법이 있다.
     ```js
     var add = new Function('x', 'y', 'return x+y');
     console.log(add(2,5));  //7
     ```
  * 화살표 함수(arrow function) : ES6에서 도입되었고 function 키워드 대신 화살표를 사용해 좀 더 간략한 방법으로 함수를 선언할 수 있다. 화살표 함수는 항상 익명 함수로 정의한다. 
    ```js
    const add = (x, y) => x + y;
    console.log(add(2,5)); // 7
    ```
- 함수 호출
  * 매개변수와 인수 : 매개변수를 통해 인수를 전달한다. 인수는 함수를 호출할 때 지정하며, 개수와 타입에 제한이 없다. 함수는 매개변수의 개수와 인수의 개수가 일치하는지 체크하지 안흔다. 인수가 부족해서 인수가 할당되지 않은 매개변수의 값은 undefined다. 매개변수보다 인수가 더 많은 경우 초과된 인수는 무시된다. 
  * 매개변수와 최대 개수 : 이상적인 함수는 한 가지 일만 해야 하며 가급적 작게 만들어야 한다. 매개변수는 최대 3개 이상을 넘지 않는 것을 권장한다. 만약 그 이 상의 매개변수가 필요하다면 하나의 매개변수를 선언하고 객체를 인수로 전달하는 것이 유리하다.
  * 반환문
    + 반환문은 함수의 실행을 중단하고 함수 몸체를 빠져나간다. 따라서 반환문 이후에 다른 문이 존재하면 그 문은 실행되지 않고 무시된다.
    + 반환문은 return 키워드 뒤에 오는 표현식을 평가해 반환한다. return 키워드 뒤에 반환값으로 사용할 표현식을 명시적으로 지정하지 않으면 undefined가 반환된다. 
- 참조에 의한 전달과 외부 상태의 변경 : 외부 상태를 변경하지 않고 외부 상태에 의존하지도 않는 함수를 순수 함수라 한다. 순수 함수를 통해 부수 효과를 최대한 억제하여 오류를 피하고 프로그램의 안정성을 높이려는 프로그래밍 패러다임을 함수형 프로그래밍이라 한다.
- 다양한 함수의 형태
  * 즉시 실행 함수 : 함수 정의와 동시에 즉시 실행되는 함수를 즉시 실행 함수라고 하며, 이는 단 한 번만 호출되며 다시 호출할 수 없다. 즉시 실행 함수는 반드시 그룹 연산자 (...)로 감싸야 한다. 즉시 실행 함수 내에 코드를 모아 두면 혹시 있을 수도 있는 변수나 함수 이름의 충돌을 방지할 수 있다.
  * 재귀 함수 : 함수가 자기 자신을 호출하는 것을 재귀 호출이라 한다. 재귀 함수는 자기 자신을 호출하는 행위, 즉 재귀 호출을 수행하는 함수를 말한다. 자기 자신을 호출하는 재귀 함수를 사용하면 반복되는 처리를 반복문 없이 구현할 수 있다. 재귀 함수 내에는 재귀 호출을 멈출 수 있는 탈출 조건을 반드시 만들어야 한다. 찰출 조건이 없으면 함수가 무한 호출되어 스택 오버플로 에러가 발생한다. 
   ```js
   function factorial(n) {
     // 탈출 조건 : n이 1 이하일 때 재귀 호출을 멈춘다.
     if (n<=1) return 1;
     // 재귀 호출
     return n * factorial(n-1);
   }
   
   console.log(factorial(5)); // 5! = 5*4*3*2*1 = 120
   ```
  * 중첩 함수 : 함수 내부에 정의된 함수를 중첩 함수 또는 내부 함수라 한다. 그리고 중첩 함수를 포함하는 함수는 외부 함수라 부른다. 중첩 함수는 외부 함수 내부에서만 호출할 수 있다. 일반적으로 중첩 함수는 자신을 포함하는 외부 함수를 돕는 헬퍼 함수의 역할을 한다. 
  * 콜백 함수 : 함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 콜백 함수라고 하며, 매개변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수를 고차 함수라고 한다. 고차 함수는 콜백 함수를 자신의 일부분으로 합성한다. 고차 함수는 매개변수를 통해 전달받은 콜백 함수의 호출 시점을 결정해서 호출한다. 콜백 함수는 고차 함수에 의해 호출되며 이때 고차 함수는 필요에 따라 콜백 함수에 인수를 전달할 수 있다. 함수형 패러다임, 비동기 처리(이벤트 처리, Ajax 통신, 타이머 함수 등)에 활용되는 중요한 패턴이다.
  ```js
  function repeat(n, f) {
    for (var i =0; i < n; i++) {
      f(i);
    }
  }

  var logOdds = function (i) {
     if (i % 2) console.log(i);
   };

  repeat(5, logOdds);
  ```
- 함수형 프로그래밍은 순수 함수와 보조 함수의 조합을 통해 외부 상태를 변경하는 부수 효과를 최소화해서 불변성을 지향하는 프로그래밍 패러다임이다. 로직 내에 존재하는 조건문과 반복문을 제거해서 복잡성을 해결하며, 변수 사용을 억제하거나 생명주기를 최소화해서 상태 변경을 피해 오류를 최소화하는 것을 목표로 한다. 

## 스코프
스코프(scope, 유효범위)는 식별자가 유효한 범위를 말한다. 모든 식별자(변수 이름, 함수 이름, 클래스 이름 등)는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정된다. 스코프란 자바스크립트 엔진이 식별자를 검색할 때 사용하는 규칙이라고도 할 수 있다. 프로그래밍 언어에서는 스코프(유효 범위)를 통해 식별자인 변수 이름의 충돌을 방지하여 같은 이름의 변수를 사용할 수 있게 한다. 스코프 내에서 식별자는 유일해야 하지만 다른 스코프에서 같은 이름의 식별자를 사용할 수 있다. 즉, 스코프는 네임스페이스다.
> 코드가 어디서 실행되며 주변에 어떤 코드가 있는지를 렉시컬 환경이라고 부른다. 즉, 코드의 문맥은 렉시컬 환경으로 이뤄진다. 이를 구현한 것이 실행 컨텍스트(execution context)이며 모든 코드는 실행 컨텍스트에서 평가되고 실행된다. 

```js
var x = 'global';  //전역 스코프

function foo() {
  var x = 'local';  // foo 함수 스코프
  console.log(x);  // local
}

foo();

console.log(x);  //global
```
전역 변수는 어디서든지 참조할 수 있다. 지역 변수는 지역 스코프와 하위 지역 스코프에서 유효하다. 
- 렉시컬 스코프
  * 자바스크립트를 비롯한 대부분의 프로그래밍 언어는 동적 스코프가 아닌 렉시컬 스코프를 따른다. 함수가 호출된 위치는 상위 스코프 결정에 어떠한 영향도 주지 않는다. 즉, 함수의 상위 스코프는 언제나 자신이 정의된 스코프다. 
  > 렉시컬 스코프(함수를 어디서 정의했는지에 따라 함수의 상위 스코프를 정의한다) vs 동적 스코프(함수를 어디서 호출했는지에 따라 함수의 상위 스코프를 정의한다)    
 ```js
 var x = 1;
function foo() {
  var x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1
```

## 전역 변수의 문제점
전역 변수의 무분별한 사용은 위험하므로, 되도록 지역 변수를 사용한다.
- 지역 변수의 생명주기 : 지역 변수의 생명주기는 함수의 생명 주기와 일치한다. 
  ```js
  function foo() {
    var x = 'local'; //변수 x 생성
    console.log(x);
    return x; //변수 x 소멸
  }
  ```
- 전역 변수의 생명주기 : 브라우저 환경에서 전역 객체는 window이므로 브라우저 환경에서 var 키워드로 선언한 전역 변수는 전역 객체 window 프로퍼티다. 전역 객체 window는 웹페이지를 닫기 전까지 유효하다. 따라서 브라우저 환경에서 var 키워드로 선언한 전역 변수는 웹페이지를 닫을 때까지 유효하다. 즉, var 키워드로 선언한 전역 변수의 생명 주기는 전역 객체의 생명 주기와 일치한다.
- 전역 변수의 사용을 억제하는 방법
  * 즉시 실행 함수 : 모든 코드를 '즉시 실행 함수'로 감싸면 모든 변수는 '즉시 실행 함수'의 지역 변수가 된다. 이 방법을 사용하면 전역 변수를 생성하지 않으므로 라이브러리 등에 자주 사용된다.
  ```js
  (function() {
    var foo = 10;
    //...
  }());
  
  console.log(foo);  //ReferenceError: foo is not defined
  ```
  
  * 네임스페이스 객체 : 전역에 네임스페이스 역할을 담당할 객체를 생성하고 전역 변수처럼 사용하고 싶은 변수를 프로퍼티로 추가하는 방법이다. 
  ```js
  var MYAPP = {}; //전역 네임스페이스 객체
  MYAPP.name = 'Lee';
  console.log(MYAPP.name); //Lee
  ```
- 모듈 패턴 : 모듈 패턴은 클래스를 모방해서 관련이 있는 변수와 함수를 모아 '즉시 실행 함수'로 감싸 하나의 모듈을 만드는 것이다. 모듈 패턴의 특징은 전역 변수의 억제는 물론 캡슐화까지 구현할 수 있다는 것이다. 즉시 실행 함수에서 객체를 반환하면, 이 객체에는 외부에 노출하고 싶은 변수나 함수를 담아 반환한다. 이때 반환되는 객체의 프로퍼티는 외부에 노출되는 public member다. 외부로 노출하고 싶지 않은 변수나 함수는 반환하는 객체에 추가하지 않으면 외부에서 접근할 수 없는 private member가 된다.
 > 캡슐화는 객체의 프로퍼티와 메서드를 하나로 묶는 것을 말한다. 캡슐화는 객체의 특정 프로퍼티나 메서드를 감출 목적으로 사용하기도 하는데 이를 정보 은닉이라 한다.
 ```js
 var Counter = (function () {
  //private 함수
  var num = 0;
  
  //외부로 공개할 데이터나 메서드를 프로퍼티로 추가한 객체를 반환한다.
  return {
    increase() {
      return ++num;
    },
  };
}());

console.log(Counter.num);  //undefined
console.log(Counter.increase());  //1
```
- ES6 모듈 : ES6 모듈을 사용하면 더는 전역 변수를 사용할 수 없다. ES6 모듈은 파일 자체의 독자적인 모듈 스코프를 제공한다. 따라서 모듈 내에서 var 키워드로 선언한 변수는 더는 전역 변수가 아니며 window 객체의 프로퍼티도 아니다. script 태그에 type="module" 속성을 추가하면 로드된 자바스크립트 파일은 모듈로서 동작한다. 모듈의 파일 확장자는 mjs를 권장한다.
```html
<script type="module" src="lib.mjs"></script>
```
  
## let, const 키워드와 블록 레벨 스코프
- let 키워드
  * 변수 중복 선언 금지
  * 블록 레벨 스코프 
  * 변수 호이스팅 발생하지 않는 것처럼 동작한다.
  * 전역 객체와 let :let 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다(즉, window.foo와 같이 접근할 수 없다). let 전역 변수는 보이지 안흔 개념적인 블록(전역 렉시컬 환경의 선언적 환경 레코드) 내에 존재하게 된다.
- const 키워드
  * 선언과 초기화 : const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 한다. 
  ```js
  const foo = 1;
  const bar; //"SyntaxError: Missing initializer in const declaration
  ```
  * 재할당 금지 : var과 let 키워드로 선언한 변수는 재할당이 자유로우나 const 키워드 선언한 변수는 재할당이 금지된다. 
  * 상수 : 상수는 재할당이 금지된 변수를 말한다. 상수는 상태 유지와 가독성, 유지보수의 편의를 위해 적극적으로 사용해야 한다. 
  * const 키워드와 객체 : const 키워드로 선언된 변수에 객체를 할당한 경우 값을 변경할 수 있다. 
  ```js
  const person  = {
    name : 'Lee'
  };
  //객체는 변경 가능한 값이다. 따라서 재할당 없이 변경이 가능하다.
  person.name = 'Kim';
  ```
- 변수 선언에 기본적으로 const를 사용하고 let은 재할당이 필요한 경우에 한정해 사용하는 것이 좋다. 

## 프로퍼티 어트리뷰트
- 내부 슬롯과 내부 메서드 : 내부 슬롯과 내부 메서드는 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 ECMAScript 사양에서 사용하는 의사 프로퍼티와 의사 메서드다. 이중 대괄호로 \[\[...]] 감싼 이름들이 내부 슬롯과 내부 메서드다.
- 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체 : 자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티 어트리뷰트(value 프로퍼티의 값, writable 값의 갱신 가능 여부, enumerable 열거 가능 여부, configurable 재정의 가능 여부)를 기본값으로 자동 정의한다. 프로퍼티 어트리뷰트에 직접 접근할 수 없지만 Object.getOwnPropertyDesciptor 메서드를 사용하여 간접적으로 확인할 수는 있다.
- 
  ```js
  const person  = {
  name : 'Lee'
  };
  //프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체를 반환한다. 첫 번째 매개변수에는 객체의 참조를 전달하고, 두번째 매개변수에는 프로퍼티 키를 문자열로 전달한다. 
  console.log(Object.getOwnPropertyDescriptor(person, 'name'));
  console.log(Object.getOwnPropertyDescriptors(person));
  //[object Object] {configurable: true, enumerable: true, value: "Lee",  writable: true}
  ```
- 데이터 프로퍼티와 접근자 프로퍼티
  * 데이터 프로퍼티(data property) : 키와 값으로 구성된 일반적인 프로퍼티다. 지금까지 살펴본 모든 프로퍼티는 데이터 프로퍼티다.
    + [[value]], [[Writable]], [[Enumerable]], [[Configurable]]
  * 접근자 프로퍼티(accessor property) : 자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티다. 접근자 프로퍼티는 다음과 같은 프로퍼티 어트리뷰트를 갖는다.
    + [[Get]] : 접근자 프로러티를 통해 데이터 프로퍼티의 값을 읽을 때 호출되는 접근자 함수다. 즉, 접근자 프로퍼티 키로 프로퍼티 값에 접근하면 프로퍼티 어트리뷰트 [[Get]]의 값, 즉 getter 함수가 호출되고 그 결과가 프로퍼티 값으로 반환된다.
    + [[Set]] : 접근자 프로러티를 통해 데이터 프로퍼티의 값을 저장할 때 호출되는 접근자 함수다. 즉, 접근자 프로퍼티 키로 프로퍼티 값에 저장하면 프로퍼티 어트리뷰트 [[Set]]의 값, 즉 setter 함수가 호출되고 그 결과가 프로퍼티 값으로 반환된다. 
    + [[Enumerable]]
    + [[Configurable]]
     ```js
     const person  = {
       //데이터 프로퍼티
       firstName: 'Marco',
       lastName: 'Jang',

       //fullName은 접근자 함수로 구성된 접근자 프로퍼티다.
       get fullName() {
         return `${this.firstName} ${this.lastName}`;
       },

       set fullName(name) {
         [this.firstName, this.lastName] = name.split(' ');
       }
     };
     // 데이터 프로퍼티를 통한 프로퍼티 값의 참조
     console.log(person.firstName + ' ' +person.lastName);   //"Marco Jang"

     // 접근자 프로퍼티를 통한 프로퍼티 값의 저장
     // 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
     person.fullName = "Gildong Hong";
     console.log(person);  //[object Object] { firstName: "Gildong", fullName: "Gildong Hong",lastName: "Hong"}

     //접근자 프로퍼티 fullName에 접근하면 getter 함수가 호출된다.
     console.log(person.fullName);  //"Gildong Hong"

     // 데이터 프로퍼티의 어트리뷰트
     let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');
     console.log(descriptor);  //[object Object] {configurable: true, enumerable: true, value: "Gildong", writable: true}

     // 접근자 프로퍼티 어트리뷰트
     descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
     console.log(descriptor);  //[object Object] {configurable: true,enumerable: true, get: get fullName() { return `${this.firstName} ${this.lastName}`;},set: set fullName(name) {[this.firstName, this.lastName] = name.split(' ');}}
     ```
   > 프로토타입 : 프로토타입은 어떤 객체의 상위 객체의 역할을 하는 객체다. 프로토타입은 하위 객체에게 자신의 프로퍼티와 메서드를 상속한다. 객체의 프로퍼티나 메서드에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티 또는 메서드가 없다면 프로토타입 체인을 따라 프로토타입의 프로퍼티나 메서드를 차례대로 검색한다. 
- 프로퍼티 정의 : Object.defineProperty 메서드를 사용하면 프로퍼티의 어트리뷰를 정의할 수 있다. 인수로는 객체의 참조와 데이터 프로퍼티의 키인 문자열, 프로퍼티 디스크립터 객체를 전달한다. 어트리뷰트를 생략할 경우 기본값으로 undefined나 false가 적용된다. 
  ```js
  const person = {};
  // 데이터 프로퍼티 정의
  Object.defineProperty(person, 'firstName', {
    value: 'Marco',
    writable: true,
    enumerable: true,
    configurable: true
  });
  
  // 접근자 프로퍼티 정의
  Object.defineProperty(person, 'fullName', {
    get() {
      return `${this.firstName} ${this.lastName}`;
    },
    set() {
      [this.firstName, this.lastName] = name.split(' ');
    },
    enumerable: true,
    configuralbe: true
  });
  ```
- 객체 변경 방지 메서드
  * 객체 확장 금지 : Object.preventExtensions, 확장이 금지된 객체는 프로퍼티 추가가 금지된다.
  * 객체 밀봉 : Object.seal, 밀봉된 객체는 읽기와 쓰기만 가능하다
  * 객체 동결 : Object.freeze, 동결된 객체는 읽기만 가능하다. 


## 생성자 함수에 의한 객체 생성 
- Object 생성자 함수 
  ```js
  const person = new Object();
  ```
  > 생성자 함수(constructor)란 new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수를 말한다. 생성자 함수에 의해 생성된 객체를 인스턴스라 한다. Object 이외에도 String, Number, Boolean, Function, Array, Date, RegExp, Promise 등의 빌트인 생성자 함수가 있다.
- 생성자 함수에 의한 객체 생성 방식의 장점 : 생성자 함수에 의한 객체 생성 방식은 마치 객체(인스턴스)를 생성하기 위한 템플릿(클래스)처럼 생성자 함수를 사용하여 프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있다. 
  ```js
  // 생성자 함수
  function Circle(radius) {
    // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
    this.radius = radius;
    this.getDiameter = function() {
      return 2*this.radius;
    };
  }
  
  //인스턴스의 생성
  const circle1 = new Circle(5);
  const circle2 = new Circle(10);
  
  //new 연산자와 함게 호출하지 않으면 그냥 일반 함수로서 호출된다.
  const circle3 = Circle(15);
  console.log(circle3) ; //일반 함수로서 호출되면 반환문이 없어 undefined가 반환된다.
  ```
  > this : this는 객체 자신의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수다. this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 따라 동적으로 결정된다.
    - 일반 함수로서 호출 : this가 가리키는 값은 '전역 객체'
    - 메서드로서 호출 : this가 가리키는 값은 '메서드를 호출한 객체(마침표 앞의 객체)'
    - 생성자 함수로서 호출 : this가 가리키는 값은 '생성자 함수가 (미래에) 생성할 인스턴스'   
- 내부 메서드 [[Call]]과 [[Construct]]
  * 함수는 객체이지만 일반 객체와 달리 호출할 수 있다. 함수가 일반 함수로서 호출되면 내부 메서드 [[Call]]이 호출되고 new 연산자와 함께 생성자 함수로서 호출되면 내부 메서드 [[Construct]]가 호출된다. 모든 함수 객체는 호출할 수 있지만, 모든 함수 객체를 생성자 함수로서 호출할 수 있는 것은 아니다. 
  ```js
  function foo() {}
  
  foo(); //일반 함수로서 [[Call]]호출
  new foo(); //생성자 함수로서 [[Construct]]호출
  ```
  * constructor와 non-constructor의 구분 
    + constructor : 함수 선언문, 함수 표현식, 클래스(클래스도 함수다)
    + non-constructor : 메서드(ES6 메서드 축약 표현), 화살표 함수
  * new 연산자 : 일반 함수와 생성자 함수에 특별한 형식적 차이는 없다. new 연산자와 함께 함수를 호출하면 해당 함수는 생성자 함수로 동작한다. 다시 말해, 함수 객체의 내부 메서드 [[Call]]이 호출되는 것이 아니라 [[Construct]]가 호출된다. 
  * new.target : new 연산자 없이 생성자 함수를 호출하여도 new.target을 통해 생성자 함수로서 호출된다.
    ```js
    // 생성자 함수
    function Circle(radius) {
      //이 함수가 new 연산자와 함께 호출되지 않았다면 new.target은 undefined다.
      if(!new.target) {
        // new 연산자와 함께 생성자 함수를 재귀 호출하여 생성된 인스턴스를 반환한다.
        return new Circle(radius);
      }

      this.radius = radius;
      this.getDiameter = function() {
        return 2 * this.radius;
      };
    }

    // new 연산자 없이 생성자 함수를 호출하여도 new.target을 통해 생성자 함수로서 호출된다.
    const circle = Circle(5);
    console.log(circle.getDiameter());
    ```
## 함수와 일급 객체
- 다음과 같은 조건을 만족하는 객체를 일급 객체라 한다. 자바스크립트의 함수는 다음 조건을 모두 만족하므로 일급 객체다. 함수가 일급 객체라는 것은 함수를 객체와 동일하게 사용할 수 있다는 것이다. 함수는 객체이지만 일반 객체와 차이가 있다. 일반 객체는 호출할 수 없지만 함수 객체는 호출할 수 있고, 함수 객체는 일반 객체에는 없는 ㅎ마수 고유의 프로퍼티를 소유한다. 
  1. 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
  2. 변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
  3. 함수의 매개변수에 전달할 수 있다.
  4. 함수의 반환값으로 사용할 수 있다.
  
- arguments 프로퍼티 
  * arguments객체는 매개변수 개수를 확정할 수 없는 가변 인자 함수를 구현할 때 유용하다.
    ```js
    function sum() {
      let res = 0;
      // arguments 객체는 유사 배열 객체이므로 for 문으로 순회 가능함
      for (let i =0; i < arguments.length; i++) {
        res += arguments[i];
      }

      return res;
    }

    console.log(sum(1,2)); //3
    console.log(sum(1,2,3)); //6
    ```
      + 유사 배열 객체는 배열이 아니므로 배열 메서드를 사용하면 에러가 발생한다. 따라서 배열 메서드를 사용하려면 간접 호출을 할 수 있다.
      ```js
      function sum() {
        //arguments 객체를 배열로 변환(간접호출)
        const array = Array.prototype.slice.call(arguments);
        return array.reduce(function(pre, cur){
          return pre+cur;
        }, 0);
      }

      console.log(sum(1,2)); //3
      console.log(sum(1,2,3)); //6
      ```
      + 이러한 번거로움을 해결하기 위해 ES6에서는 Rest 파라미터를 도입했다.
      ```js
      function sum(...args) {
        return args.reduce((pre,cur) => pre+cur, 0);
      }

      console.log(sum(1,2)); //3
      console.log(sum(1,2,3)); //6
      ```

## 프로토타입
- 객체지향 프로그래밍 : 프로그램을 명령어 또는 함수의 목록으로 보는 전통적인 명령형 프로그래밍의 절차지향적 관점에서 벗어나 여러 개의 독립적 단위, 즉 객체(object)의 집합으로 프로그램을 표현하려는 프로그래밍 패러다임을 말한다. 객체
- 상속과 프로토타입 : 상속은 객체지향 프로그래밍의 핵심 개념으로, 어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속받아 그대로 사용할 수 있는 것을 말한다. 자바스크립트는 프로토타입을 기반으로 상속을 구현한다. 상속을 통해 불필요한 중복을 제거해 보자.
  > 자신의 상태를 나타내는 radius 프로퍼티만 개별적으로 소유하고 내용이 동일한 메서드는 상속을 통해 공유하여 사용한다.
  ```js
  //생성자 함수
  function Circle(radius) {
    this.radius = radius;
    //Circle 생성자 함수가 생성한 모든 인스턴스가 getArea 메서드를 공유해서 사용할 수 있도록 프로토타입에 추가
    Circle.prototype.getArea = function() { //this.getArea 가 아니라 Circle.prototype.getArea
      return Math.PI * this.radius ** 2;
    };
  }

  const circle1 = new Circle(1);
  const circle2 = new Circle(2);

  //Circle 생성자 함수가 생성하는 모든 인스터스는 하나의 getArea 메서드를 공유한다.
  console.log(circle1.getArea === circle2.getArea); //true
  console.log(circle1.getArea()); //3.141592653589793
  console.log(circle2.getArea()); //12.566370614359172
  ```
  > Object.prototype : 모든 객체는 프로토타입의 계층 구조인 프로토타입 체인에 묶여 있다. 자바스크립트 엔진은 객체의 프로퍼티에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 \_\_protto__ 접근자 프로퍼티가 가리키는 참조를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다. 프로토타입 체인의 종점, 최상위 객체는 Object.prototype이며, 이 객체의 프로퍼티와 메서드는 모든 객체에 상속된다. 
- 프로토타입은 생성자 함수가 생성되는 시점에 더불어 생성된다. 둘은 언제나 쌍으로 존재한다. 
- 인스턴스에 의한 프로토타입의 교체
  ```js
  function Person(name) {
    this.name = name;
  }

  const me = new Person('Lee');

  //프로토타입으로 교체할 객체
  const parent = {
    sayHello() {
      console.log(`Hi! My name is ${this.name}`);
    }
  };

  //me  객체의 프로토타입을 parent 객체로 교체한다.
  Object.setPrototypeOf(me, parent);
  // 위 코드는 아래 코드와 동일하게 동작한다.
  // me.__proto__ = parent;

  me.sayHello(); //"Hi! My name is Lee"
  ```
- 직접 상속
  * Object.create에 의한 직접 상속 : Object.create 메서드의 첫 번째 매개변수에는 생성할 객체의 프로토타입으로 지정할 객체를 전달한다. 두 번째 매개변수에는 생성할 객체의 프로퍼티 키와 프로퍼티 디스크립터 객체로 이뤄진 객체를 전달하며, 두 번째 인수는 옵션이므로 생략 가능하다.
  ```js
  obj = Object.create(Object.prototype, {
    x: {value: 1, writable: true, enumerable: true, configurable: true}
  });
  // 위 코드는 아래와 동일하다.
  // obj = Object.create(Object.prototype);
  // obj.x = 1;
  ```
  * 객체 리터럴 내부에서 \_\_proto__에 의한 상속(ES6)
  ```js
  const myProto = {x:10};
  const obj = {
    y: 20,
    __proto__ : myProto
  };
  console.log(obj.x, obj.y); //10 20
  ```
  
- 프로퍼티 존재 확인
  * in 연산자 : 객체 내에 특정 프로퍼티가 존재하는지 여부 확인
  ```js
  key in object
  //ES6에서는 Refelect.has 메서드 사용 가능
  Reflect.has(object, key)
  ```
  * Object.prototype.hasOwnProperty 메서드 : 객체 내에 특정 프로퍼티가 존재하는지 확인할 수 있고, 객체 고유의 프로퍼티 키인 경우에만 true를 반환한다(상속받은 프로토타입의 프로퍼티 키인 경우 false반환).
- 프로퍼티 열거
  * for ... in 문
  ```js
  const person = {
    name: 'Marco',
    address: 'Seoul',
    __proto__: {age:20}
  };

  for (const key in person) {
  // 객체 자신의 프로퍼티인지 확인한다.
    if(!person.hasOwnProperty(key)) continue;
    console.log(key + ': ' + person[key]);
  }
  //"name: Marco"
  //"address: Seoul"
  ```
  * Object.keys/values/entries 메서드 : 객체 자신의 고유 프로퍼티만 열거
  ```js
  const person = {
    name: 'Marco',
    address: 'Seoul',
    __proto__: {age:20}
  };

  console.log(Object.keys(person));  //["name", "address"]
  console.log(Object.values(person));  //["Marco", "Seoul"]
  console.log(Object.entries(person));  //[["name", "Marco"], ["address", "Seoul"]]
  ```
## 빌트인 객체
- 표준 빌트인 객체 : 자바스크립트는 Object, String, Number, Boolean, Symbol, Date, Math, Array, Map/Set, WeakMap/WeakSet, Function, Promise, Reflect, Proxy, JSON, Error 등 40여 개의 표준 빌트인 객체를 제공한다. Math, Reflect, JSON을 제외한 나머지는 모두 인스턴스를 생성할 수 있는 생성자 함수 객체다. 
- 전역 객체: 전역 객체는 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체이며, 어떤 객체에도 속하지 않은 최상위 객체다. 브라우저 환경에서는 window(또는 self, this, frames)가 전역 객체를 가리키지만 Node.js 환경에서는 global 전역 객체를 가리킨다. ES11에서 도입된 globlaThis는 브라우저 환경과 Node.js 환경에서 전역 객체를 가리키던 다양한 식별자를 통일한 식별자다. 
- 빌트인 전역 함수 : 애플리케이션 전역에서 호출할 수 있는 빌트인 함수로서 전역 객체의 메서드다.
  * eval : eval 함수는 코드를 나타내는 문자열을 인수로 전달받는다. eval 함수를 통해 사용자로부터 입력받은 콘텐츠를 실행하는 것은 보안에 매우 취약하고 최적화가 수행되지 않으므로, eval 함수 사용은 금지해야 한다. 
  * isFinite
  * isNaN
  * parseFloat
  * parseInt
  * encodeURI / decodeURI : 완전한 URI를 문자열로 전달받아 이스케이프(어떤 시스템에서도 읽을 수 있는 아스키 문자 셋으로 변환) 처리를 위해 인코딩/디코딩한다.

## this

- this 키워드
    - this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수다. this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다. ths는 자바스크립트 엔진에 의해 암묵적으로 생성되며, 코드 어디서든 호출할 수 있다. this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 동적으로 결정된다.
        - this 바인딩 : 바인딩이란 식별자와 값을 연결하는 과정을 의미한다. this 바인딩은 this(키워드로 분류되지만 식별자 역할을 한다)와 this가 가리킬 객체를 바인딩하는 것이다.
    
    ```jsx
    function Circle(radius) {
      //this는 생성자 함수가 생성할 인스턴스를 가리킨다.
      this.radius  = radius;
    }
    Circle.prototype.getDiameter = function() {
      //this는 생성자 함수가 생성할 인스턴스를 가리킨다.
      return 2*this.radius;
    }
    
    // 인스턴스 생성
    const circle = new Circle(5);
    console.log(circle.getDiameter());
    ```
    
- 함수 호출 방식과 this 바인딩
    - this 바인딩(this에 바인딩될 값)은 함수 호출 방식, 즉 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다. this바인딩은 함수 호출 시점에 결정된다.
    - 일반 함수로 호출된 모든 함수(중첩 함수, 콜백 함수 포함) 내부의 this에는 전역 객체가 바인딩된다.
        
        ```jsx
        var value = 1;
        
        const obj = {
          value: 100,
          foo() {
            console.log("foo's this: ", this); // foo's this:  {value: 100, foo: ƒ}
            console.log("foo's this.value: ", this.value); //foo's this.value:  100
        
            function bar() {
              console.log("bar's this: ", this); //bar's this:  Window {0: Window, 1: global, window: Window, self: Window, document: document, name: '', location: Location, …}
              console.log("bar's this.value: ", this.value); //bar's this.value:  1
            }
        
            bar();
          },
        };
        
        obj.foo();
        ```
        
    - 메서드 내부의 중첩 함수나 콜백 함수의 this 바인딩을 메서드의 this 바인딩과 일치시키기 위한 방법은 다음과 같다.
        - this 바인딩을 변수 that에 할당
            
            ```jsx
            var value = 1;
            
            const obj = {
              value: 100,
              foo() {
                const that = this;  //this 바인딩(obj)을 변수 that에 할당한다.
                console.log("foo's this: ", that);  // foo's this:  {value: 100, foo: ƒ}
                console.log("foo's this.value: ", that.value); //foo's this.value:  100
            
                function bar() {
                  console.log("bar's this: ", that); // bar's this:  {value: 100, foo: ƒ}
                  console.log("bar's this.value: ", that.value);  //bar's this.value:  100
                }
                bar();
              },
            };
            
            obj.foo();
            ```
            
        - bind 메서드
            
            ```jsx
            var value = 1;
            
            const obj = {
              value: 100,
              foo() {
            		//콜백 함수에 명시적으로 this를 바인딩한다
                setTimeout(
                  function () {
                    console.log(this.value);
                  }.bind(this),
                  100
                );
              },
            };
            
            obj.foo();
            ```
            
    - Function.prototype.apply/call/bind 메서드에 의한 간접 호출
        - this로 사용할 객체와 인수 리스트를 인수로 전달받아 함수로 호출한다. apply와 call 메서드의 본질적인 기능은 함수를 호출하는 것이다.
            
            ```jsx
            function getThisBinding() {
              console.log(arguments);
              return this;
            }
            
            const thisArg = {a:1};
            
            //apply 메서드는 호출할 함수의 인수를 배열로 묶어 전달한다
            console.log("1", getThisBinding.apply(thisArg, [1,2,3]));
            //call 메서드는 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달한다
            console.log("2", getThisBinding.call(thisArg, 1, 2, 3));
            ```
            
        - bind 메서드는 this로 사용하라 객체만 전달한다. 함수를 호출하지는 않으므로 명시적으로 호출해야 한다. bind 메서드는 메서드의 this와 메서드 내부의 중첩 함수 또는 콜백 함수의 this가 불일치하는 문제를 해결하기 위해 유용하게 사용된다.
            
            ```jsx
            function getThisBinding() {
              return this;
            }
            
            const thisArg = {a:1};
            
            console.log(getThisBinding.bind(thisArg)); //function () { [native code] }
            //함수를 호출하지는 않으므로 명시적으로 호출해야 한다.
            console.log(getThisBinding.bind(thisArg)()); //[object Object] { a: 1}
            ```
            
            ```jsx
            const person = {
              name: 'Marco',
              foo(callback) {
                //bind메서드로 callback 함수 내부의 this 바인딩을 전달
                setTimeout(callback.bind(this), 100);
              }
            };
            
            person.foo(function() {
              //위에서 bind 메서드를 사용하지 않았다면 일반 함수로 호출된 콜백 함수 내부의 this.name은 브라우저 환경에서 window.name과 같다.
              console.log(`hi! my name is ${this.name}`);
            })
            ```
            
            - 일반 함수 호출 → this바인딩 : 전역객체
            - 메서드 호출 → this 바인딩: 메서드를 호출한 객체
            - 생성자 함수 호출 → this바인딩 : 생성자 함수가 미래에 생성할 인스턴스
            - Function.prototype.apply/call/bind메서드에 의한 간접 호출 → Function.prototype.apply/call/bind 메서드에 첫번째 인수로 전달한 객체

## 실행 컨텍스트

- 소스코드의 4가지 타입 → 실행 컨텍스트를 생성하는 과정과 관리 내용이 다름
    1. 전역 코드 : 전역에 존재하는 소스코드(전역에 정의된 함수, 클래스 등의 내부 코드는 비포함)
    2. 함수 코드 : 함수 내부에 존재하는 소스코드(함수 내부에 중첩된 함수, 클래스 등의 내부 코드는 비포함)
    3. eval 코드 : 빌트인 전역 함수인 eval 함수에 인수로 전달되어 실행되는 소스코드
    4. 모듈 코드 : 모듈 내부에 존재하는 소스코드(모듈 내부의 함수, 클래스 등의 내부 코드는 비포함)
- 소스코드의 평가와 실행 : 자바스크립트 엔진은 소스코드를 평가와 실행으로 나누어 처리한다.
    - 소스코드 평가  : 실행 컨텍스스트 생성하고 변수, 함수 등의 선언문만 먼저 실행하여 생성된 변수나 함수 식별자를 키로 실행 컨텍스트가 관리하는 스코프(렉시컬 환경의 환경 레코드)에 등록한다.
    - 소스코드 실행 : 평가가 끝나면 비로서 선언문을 제외한 소스코드가 순차적으로 실행된다(런타임 시작). 이때 소스코드 실행에 필요한 정보, 즉 변수나 함수의 참조를 실행 컨텍스트가 관리하는 스코프에서 검색해서 취득한다. 그리고 변수 값의 변경 등 소스코드의 실행 결과는 다시 실행 컨텍스트가 관리하는 스코프에 등록된다.
- 실행 컨텍스트는 식별자(변수, 함수, 클래스 등의 이름)를 등록하고 관리하는 스코프와 코드 실행 순서 관리를 구현한 내부 메커니즘으로, 모든 코드는 실행 컨텍스트를 통해 실행되고 관리된다. 식별자와 스코프는 실행 컨텍스트의 `렉시컬 환경`으로 관리하고 코드 실행 순서는 `실행 컨텍스트 스택`으로 관리한다.

## 클로저

클로저(closure)는 함수와 그 함수가 선언된 렉시컬 환경과의 조합이다. 

- 렉시컬 스코프
    - 자바스크립트 엔진은 함수를 어디서 호출했는지가 아니라 `함수를 어디에 정의했는지`  에 따라 상위 스코프를 결정한다. 이를 렉시컬 스코프(정적 스코프)라 한다.  함수의 상위 스코프를 결정한다는 것은 "렉시컬 환경의 외부 렉시컬 환경에 대한 참조에 저장할 참조값을 결정한다"는 것과 같다.  상위 스코프에 대한 참조는 함수 정의가 평가되는 시점에 함수가 정의된 환경(위치)에 의해 결정된다.
- 클로저와 렉시컬 환경
    - 외부 함수(아래 outer 함수)보다 중첩 함수(아래 inner 함수)가 더 오래 유지되는 경우 중첩 함수는 이미 생명 주기가 종료한 외부 함수의 변수를 참조할 수 있다. 이러한 중첩 함수를 `클로저` 라고 부른다.
    
    ```jsx
    const x = 1;
    
    function outer() { //외부 함수
      const x = 10;
      const inner = function() {console.log(x);}; //중첩 함수
      return inner;
    }
    
    const innerFunc = outer();
    	innerFunc(); //10
    ```
    
    - outer 함수의 실행 컨텍스트는 실행 컨텍스트에서 제거되지만 outer 함수의 렉시컬 환경까지 소멸하는 것은 아니다.
    - 자바스크립트의 모든 함수는 상위 스코프를 기억하므로 이론적으로 모든 함수는 클로저다. 하지만 모든 함수를 클로저라고 하지는 않는다. **클로저는 중첩 함수가 상위 스코프의 식별자를 참조하고 있고 중첩 함수가 외부 함수보다 오래 유지된 경우에 한정하는 것이 일반적이다.**
        - 상위 스코프의 어떤 식별자도 참조하지 않는 경우 대부분의 모던 브라우저는 최적화를 통해 상위 스코프를 기억하지 않는다. 이런 경우 중첩함수는 클로저라고 할 수 없다. 외부 함수보다 중첩 함수의 생명 주기가 짧은 경우 클로저라고 하지 않는다.
        - 클로저에 의해 참조되는 상위 스코프의 변수를 `자유 변수(free variable)`  라고 부른다. 클로저(closure)란 `자유 변수에 묶여있는 함수` 라고 할 수 있다.
- 클로저의 활용
    - 클로저는 상태를 안전하게 변경하고 유지하기 위해 사용한다. 상태가 의도치 않게 변경되지 않도록 상태를 안전하게 은닉하고 특정 함수에게만 상태 변경을 허용하기 위해 사용한다.
        
        ```jsx
        const counter = (function() {
          let num = 0;
          //클로저인 메서드를 갖는 개체를 반환한다.
          //객체 리터럴은 스코프를 만들지 않는다.
          //따라서 아래 메서드들의 상위 스코프는 즉시 실행 함수의 렉시컬 환경이다.
          return {
            // num:0, //프로퍼티는 pulbic 하므로 은닉되지 않는다.
            increase() {
              return ++num;
            },
            decrease() {
              return num >0 ? --num : 0;
            }
          };
        }());
        
        console.log(counter.increase()); //1
        console.log(counter.increase()); //2
        console.log(counter.decrease()); //1
        console.log(counter.decrease()); //0
        ```
        
- 캡슐화와 정보 은닉
    - 캡슐화는 객체의 상태를 나타내는 프로퍼티와 프로퍼티를 참조하고 조작할 수 있는 동작인 메서드를 하나로 묶는 것을 말한다. 캡슐화는 객체의 특정 프로퍼티나 메서드를 감출 목적으로 사용하기도 하는데 이를 정보 은닉이라 한다.
    

## 클래스

자바스크립트는 `프로토타입 기반 객체지향 언어`이다. 프로토타입 기반 객체지향 언어는 클래스가 필요 없는 객체지향 프로그래밍 언어다. 

`ES5`에서는 클래스 없이도 다음과 같이 `생성자함수` 와 `프로토타입` 을 통해 객체지향 언어의 `상속` 을 구현할 수 있다.

```jsx
 // ES5 생성자 함수
var Person = (function() {
  //생성자 함수
  function Person(name) {
    this.name = name;
  }
  
  // 프로토타입 메서드
  Person.prototype.sayHi = function() {
    console.log("Hi! My name is " + this.name);
  }
  
  // 생성자 함수 반환
  return Person;
}());

//인스턴스 생성
var me = new Person("Marco");
me.sayHi();  //"Hi! My name is Marco"
```

`ES6` 에서 도입된 클래스는 사실 함수이며 기존 프로토타입 기반 패턴을 클래스 기반 패턴처럼 사용할 수 있도록 하는 `문법적 설탕` 이라고 볼 수도 있으나, 클래스의 extends와 super 키워드는 상속 관계 구현을 더욱 간결하고 명료하게 하므로 `새로운 객체 생성 메커니즘`으로 보는 것이 좀 더 합당하다. 

- 클래스는 생성자 함수보다 엄격하며 생성자 함수에서는 제공하지 않는 기능도 제공한다.
    - 클래스를 new 연산자 없이 호출하면 에러가 발생한다. 하지만 생성자 함수를 new 연산자 없이 호출하면 일반 함수로서 호출된다.
    - 클래스는 상속을 지원하는 extends와 super 키워드를 제공한다. 하지만 생성자 함수는 extends와 super키워드를 지원하지 않는다.
    - 클래스는 호이스팅이 발생하지 않는 것처럼 동작한다. 하지만 함수 선언문으로 정의된 생성자 함수는 함수 호이스팅이, 함수 표현식으로 정의한 생성자 함수는 변수 호이스팅이 발생한다.
    - 클래스 내의 모든 코드에는 암묵적으로 strict mode가 지정되어 실행되며 strict mode를 해제할 수 없다. 하지만 생성자 함수는 암묵적으로 strict mode가 지정되지 않는다.
    - 클래스의 constructor, 프로토타입 메서드, 정적 메서드는 모두 프로퍼티 어트리뷰트 [[Enumerable]]의 값이 false다. 다시 말해, 열거되지 안흔ㄴ다.
- 클래스 정의 : class 키워드 사용, 파스칼 케이스 사용(첫글자 대문자), 일급 객체(표현식으로 정의 가능, 값으로 사용 가능)
    - 클래스 몸체에 정의할 수 있는 메서드는 constructor(생성자), 프로토타입 메서드, 정적 메서드의 세 가지가 있다.
    
    ```jsx
    //클래스 선언문
    class Person {
      //생성자
      constructor(name) {
        //인스턴스 생성 및 초기화
        this.name = name;
      }
      //프로토타입 메서드
      sayName() {
        console.log(`Hi! My name is ${this.name}`);
      }
      //정적 메서드
      static sayHello() {
        console.log('Hello!');
      }
    }
    
    //인스턴스 생성
    const me = new Person('Marco');
    
    //인스턴스의 프로토타입 참조
    console.log(me.name); //"Marco"
    //프로토타입 메서드 호출
    me.sayName(); //"Hi! My name is Marco"
    
    me.sayHello(); //"TypeError: me.sayHello is not a function
    //정적 메서드 호출
    Person.sayHello(); //"Hello!"
    ```
    
- 클래스 호이스팅
    - 클래스는 let, const 키워드로 선언한 변수처럼 호이스팅된다. 클래스 선언문 이전에 일시적 사각지대에 빠지기 때문에 호이스팅이 발생하지 않는 것처럼 동작한다. 사실 var, let, const, function, function*, class 키워드를 사용하여 선언된 모든 식별자는 호이스팅된다. 모든 선언문은 런타임 이전에 먼저 실행되기 때문이다.
- 인스턴스 생성
    - 클래스는 생성자 함수이며 `new 연산자`와 함께 호출되어 인스턴스를 생성한다.
- 메서드
    - 클래스 몸체에는 0개 이상의 메서드만 선언할 수 있다. 클래스 몸체에서 정의할 수 있는 메서드는 `constructor(생성자)`, `프로토타입 메서드`, `정적 메서드`의 세 가지가 있다.
        - `constructor` : constructor는 인스턴스를 생성하고 초기화하기 위한 특수한 메서드다. constructor는 클래스 내에 최대 한 개만 존재할 수 있고 생략할 수 있다. constructor 내부에서 return 문은 반드시 생략한다.
            - 클래스의 constructor 메서드와 프로토타입의 constructor 프로퍼티는 이름이 같아 혼동하기 쉽지만 직접적인 관련이 없다. 프로토타입의 constructor 프로퍼티는 모든 프로토타입이 가지고 있는 프로퍼티이며, 생성자 함수를 가리킨다.
        - `프로토타입 메서드` :  클래스 몸체에서 정의한 메서드는 생성자 함수에 의한 객체 생성 방식(ex, 클래스명.prototype.메서드명 = function() {)과 다르게 클래스의 prototype 프로퍼티에 메서드를 추가하지 않아도(메서드명() { ) 기본적으로 프로토타입 메서드가 된다.
        - `정적(static) 메서드` : 인스턴스를 생성하지 않아도 호출할 수 있는 메서드이다. 클래스에서는 메서드에 static 키워드를 붙이면 정적 메서드(클래스 메서드)가 된다.  정적 메서드는 프로토타입 메서드처럼 인스턴스로 호출하지 않고 클래스로 호출한다.
            - 정적 메서드와 프로토타입 메서드의 차이
                - 정적 메서드와 프로토타입 메서드는 자신이 속해 있는 프로토타입 체인이 다르다.
                - 정적 메서드는 클래스로 호출하고 프로토타입 메서드는 인스턴스로 호출한다.
                - 정적 메서드는 인스턴스 프로퍼티를 참조할 수 없지만 프로토타입 메서드는 인스턴스 프로퍼티를 참조할 수 있다.
                
                ```jsx
                class Square {
                  // 정적 메서드
                  static area(width, height) {
                    return width * height;
                  }
                }
                
                console.log(Square.area(10, 10)); //100
                ```
                
                ```jsx
                class Square {
                  constructor(width, height) {
                    this.width = width;
                    this.height = height;
                  }
                  //프로토타입 메서드
                  area() {
                    return this.width * this.height;
                  }
                }
                
                const square = new Square(10, 10);
                console.log(square.area()); //100
                ```
                
- 클래스의 인스턴스 생성 과정
    
    ```jsx
    class Person {
      // 생성자
      constructor(name) {
        //1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
        console.log(this);
        console.log(Object.getPrototypeOf(this) === Person.prototype);
        
        //2. this에 바인딩되어 있는 인스턴스를 초기화한다.
        this.name = name;
        
        //3. 완성된 인스턴스가 바인딩된 this로 암묵적으로 반환된다. 
      }
    }
    ```
    
- 상속에 의한 클래스 확장
    - 상속에 의한 클래스 확장은 기존 클래스를 상속받아 새로운 클래스를 확장(extends)하여 정의하는 것이다. 클래스는 상속을 통해 다른 클래스를 확장할 수 있는 문법인 `extends`  키워드가 기본적으로 제공된다.
    
    ```jsx
    class Animal {
      constructor(age, weight) {
        this.age = age;
        this.weight = weight;
      }
      
      eat() { return 'eat';}
      move() { return 'move';}
    }
    
    // 상속을 통해 Animal 클래스를 확장한 Bird 클래스
    class Bird extends Animal {
      fly() {return 'fly';}
    }
    
    const bird = new Bird(1, 5);
    console.log(bird); //[object Object] { age: 1, weight: 5}
    console.log(bird instanceof Bird); //true
    console.log(bird instanceof Animal); //true
    ```
    
    - 동적 상속 : extends 키워드는 클래스뿐만 아니라 생성자 함수를 상속받아 클래스를 확장할 수도 있다. 단, extends 키워드 앞에는 반드시 클래스가 와야 한다. extends 키워드 다음에는 클래스뿐만이 아니라 [[Construct]] 내부 메서드를 갖는 함수 객체로 평가될 수 있는 모든 표현식을 사용할 수 있다. 이를 통해 동적으로 상속받을 대상을 결정할 수 있다.
        
        ```jsx
        function Base1() {}
        class Base2 {}
        
        let condition = true;
        
        //조건에 따라 동적으로 상속 대상을 결정하는 서브클래스
        class Derived extends (condition ? Base1 : Base2) {}
        
        const derived = new Derived();
        console.log(derived);
        console.log(derived instanceof Base1); //true
        console.log(derived instanceof Base2); //false
        ```
        
    - super 키워드
        - `super를 호출`하면 수퍼클래스의 constructor를 호출한다.
            
            ```jsx
            class Base {
              constructor(a,b) {
                this.a = a;
                this.b = b;
              }
            }
            
            class Derived extends Base {
              constructor(a, b, c) {
                super(a, b);
                this.c = c;
              }
            }
            
            const derived = new Derived(1, 2, 3);
            console.log(derived);
            ```
            
            - super 호출 시 주의사항
                1. 서브클래스에서 constructor를 생략하지 않는 경우 서브클래스의 constructor에서는 반드시 super을 호출해야 한다.
                2. 서브클래스의 constructor에서 super를 호출하기 전에는 this를 참조할 수 없다.
                3. super는 반드시 서브클래스의 constructor에서만 호출한다. 서브클래스가 아닌 클래스의 constructor나 함수에서 super를 호출하면 에러가 발생한다.
        - `super를 참조`하면 수퍼클래스의 메서드를 호출할 수 있다.
            - 서브클래스의 프로토타입 메서드 내에서 super.sayHi는 수퍼클래스의 프로토타입 메서드 sayHi를 가리킨다.
                
                ```jsx
                //수퍼 클래스
                class Base {
                  constructor(name) {
                    this.name = name;
                  }
                  sayHi() {
                    return `Hi! ${this.name}`;
                  }
                }
                
                //서브클래스
                class Derived extends Base {
                  sayHi() {
                    //super.sayHi는 수퍼클래스의 프로토타입 메서드를 가리킨다.
                    return `${super.sayHi()}. how are you doing?`;
                  }
                }
                
                const derived = new Derived('Marco');
                console.log(derived.sayHi()); //"Hi! Marco. how are you doing?"
                ```
                

## ES6 함수의 추가 기능

- 화살표 함수(arrow function)
    - 화살표 함수는 콜백 함수 내부에서 this가 전역 객체를 가리키는 문제를 해결하기 위한 대안으로 유용한다.
    
    ```jsx
    //매개변수 여러 개인 경우(소괄호)
    const arrow = (x, y) => {...};
    //매개변수가 한 개인 경우(소괄호 생략 가능)
    const arrow = x => {...};
    //매개변수가 없는 경우(소괄호 생략 불가)
    const arrow = () => {...};
    ```
    
    - 객체 리터럴을 반환하는 경우 객체 리터럴을 소괄호()로 감싸줘야 한다.
        
        ```jsx
        const create = (id, content) => ({id, content});
        // 위 표현은 다음과 동일하다. 
        // const create = (id, content) => { return {id, content}; };
        console.log(create(1, 'Javascript')); //[object Object] { content: "Javascript",id: 1}
        ```
        
    - 화살표 함수도 `즉시 실행 함수`(IIFE) 로 사용할 수 있다.
        
        ```jsx
        const person = name => {
          return `Hi? My name is ${name}`
        };
        console.log(person("Marco"));
        
        //즉시 실행 함수로 변환
        const person = (name => {
          return `Hi? My name is ${name}`
        })("Marco");
        console.log(person);
        ```
        
    - 화살표 함수도 일급 객체이므로, `map, filter, reduce 같은 고차 함수(HOF)`에 인수로 전달할 수 있다.
        
        ```jsx
        console.log([1,2,3].map(v=>v*2)); //[2, 4, 6]
        ```
        
    - 화살표 함수와 일반 함수의 차이
        - 화살표 함수는 인스턴스를 생성할 수 없는 non-constructor이다.
        - 중복된 매개변수 이름을 선언할 수 없다.
        - 화살표 함수는 함수 자체의 this, arguments, super, [new.target](http://new.target) 바인딩을 갖지 않는다.
        - 일반함수의 `this`와 다르게 동작한다. 일반함수의 `콜백 함수 내부의 this문제` 를 해결하기 위해 ES6에서는 화살표 함수를 사용할 수 있다.
            - 화살표 함수는 함수 자체의 `this` 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 this를 참조하면 상위 스코프의 this를 그대로 참조한다. 이를 `lexical this`라 한다. 화살표 함수의 this가 함수가 정의된 위치에 의해 결정된다.
        - 화살표 함수는 함수 자체의 `super`바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 super를 참조하면 this와 마찬가지로 상위 스코프의 super를 참조한다.
        - 화살표 함수는 함수 자체의 `arguments` 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 arguments를 참조하면 this와 마찬가지로 상위 스코프의 arguments를 참조한다.
            - argumetns 객체는 함수를 정의할 때 매개변수의 개수를 확정할 수 없는 가변 인자 함수를 구현할 때 유용하다. 하지만 화살표 함수에서는 arguments 객체를 사용할 수 없다. 상위 스코프의 arguments 객체를 참조할 수는 있지만 화살표 함수 자신에게 전달된 인수 목록을 확인할 수 없고 상위 함수에게 전달된 인수 목록을 참조하므로 그다지 도움이 되지 않는다. 따라서 화살표 함수로 `가변 인자 함수`를 구현해야 할 때는 반드시 `Rest 파라미터`를 사용해야 한다.
- Rest 파라미터
    - Rest 파라미터(나머지 매개변수)는 매개변수 이름 앞에 세 개의 점 `...`을 붙여서 정의한 매개변수를 의미한다. Rest 파라미터는 함수에 전달된 인수들의 목록을 `배열` 로 전달받는다. Rest 파라미터는 이름 그대로 먼저 선언된 매개변수에 할당된 인수를 제외한 나머지 인수들로 구성된 배열이 할당된다. 따라서 Rest 파라미터는 반드시 마지막 파라미터이어야 한다. Rest파라미터는 단 하나만 선언할 수 있다.
        
        ```jsx
        function bar(param1, param2, ...rest) {
          console.log(param1);  //1
          console.log(param2); //2
          console.log(rest); //[3,4,5]
        }
        
        bar(1,2,3,4,5)
        ```
        
    - Rest 파라미터와 arguments 객체
        - ES6에서는 rest 파라미터를 사용하여 가변 인자 함수의 인수 목록을 배열로 직접 전달받을 수 있다. 이를 통해 유사 배열 객체인 arguments 객체를 배열로 변환하는 번거로움을 피할 수 있다. 화살표 함수는 함수 자체의 arguments 객체를 갖지 않으므로, 화살표 함수로 가변 함수 인자를 구현할 때는 반드시 Rest 파라미터를 사용해야 한다
            
            ```jsx
            function sum(...args) {
              // Rest 파라미터 args에는 배열 [1,2,3,4,5]가 할당된다.
              return args.reduce((pre, cur) => pre + cur, 0);
            }
            
            console.log((sum(1,2,3,4,5)));
            ```
            
- 매개변수 기본값
    - 매개변수 기본값은 매개변수에 `인수를 전달하지 않은 경우`와 `undefined`를 전달한 경우에만 유효하다.
    
    ```jsx
    function logName(name="Marco") {
      console.log(name);
    }
    
    logName(); //"Marco" 
    logName(undefined); //"Marco"
    logName(null); //null
    ```
    

## 배열

`배열(array)`이란 여러 개의 값을 `순차적`으로 나열한 자료구조다.  배열이 가지고 있는 값을 `요소(elements)` 라고 부른다. 배열의 요소에는 배열에서 자신의 위치를 나타내는 0 이상의 정수인 `인덱스(index)` 를 갖는다. 인덱스는 배열의 요소에 접근할 때 사용한다. 

- 배열은 요소의 개수, 즉 배열의 길이를 나타내는 length 프로퍼티를 갖는다. 따라서 for 문을 통해 순차적으로 요소에 접근할 수 있다.
- 배열은 객체(object) 타입이다. 그러나 일반 객체와는 구별되는 독특한 특징이 있다.
    - 객체 = ( 구조 : `프로퍼티 키와 프로퍼티 값`, 값의 참조: `프로퍼티 키`, 값의 순서: `X`, length 프로퍼티: `X`)
    - 배열 =  ( 구조 : `인덱스와 요소`, 값의 참조: `인덱스`, 값의 순서: `O`, length 프로퍼티: `O`)
- 배열은 `배열 리터럴`, `Array 생성자 함수`, `Array.of`, `Array.from` 메서드로 생성할 수 있따. 배열의 생성자 함수는 `Array` 이며, 배열의 프로토타입 객체는 `Array.prototype`  이다.
    
    ```jsx
    const arr = ['apple', 'banana', 'orange'];
    console.log(arr[0]) //apple
    console.log(arr.length) //3
    
    for (let i=0; i<arr.length; i++) {
      console.log(arr[i]); 
    }
    
    console.log(typeof arr) //"object"
    console.log(arr.constructor) // function Array() { [native code] }
    ```
    
- 자바스크립트 배열은 해시 테이블로 구현된 객체이므로 인덱스로 요소에 접근하는 경우 일반적인 배열보다 성능적인 면에서 느릴 수밖에 없는 구조적인 단점이 있다. 하지만 특정 요소를 검색하거나 요소를 삽입 또는 삭제하는 경우에는 일반적인 배열보다 빠른 성능을 기대할 수 있다.
- 배열 생성
    - `배열 리터럴` : 0개 이상의 요소를 쉼표로 구분하여 대괄호로 묶는다.
        
        ```jsx
        const arr = [1, 2, 3];
        ```
        
    - `Array 생성자 함수` : 전달된 인수의 개수에 따라 다르게 동작한다.
        - 전달된 인수가 `1개` 이고 `숫자`인 경우, length 프로퍼티 값이 인수인 배열을 생성한다.
        - 전달된 인수가 없는 경우 빈 배열을 생성한다.
        - 전달된 인수가 2개 이상이거나 숫자가 아닌 경우 인수를 요소로 갖는 배열을 생성한다.
        
        ```jsx
        const arr1 = new Array(3); //[undefined, undefined, undefined]
        console.log(arr1);
        
        const arr2 = new Array(1,2,3);
        console.log(arr2) //[1, 2, 3]
        ```
        
    - `Array.of` : 전달된 인수를 요소로 갖는 배열을 생성한다.
        
        ```jsx
        console.log(Array.of(1), Array.of(1,2,3), Array.of("Hi"));
        //[1]
        //[1, 2, 3]
        //["Hi"]
        ```
        
    - `Array.from` : 유사 배열 객체 또는 이터러블 객체를 인수로 전달받아 배열로 변환하여 반환한다.(ES6에서 도입)
        
        ```jsx
        // 유사 배열 객체를 변환하여 배열을 생성한다.
        console.log(Array.from({length: 2, 0: "a", 1: "b"})); //["a", "b"]
        ```
        
- 배열 요소의 참조
    - 배열의 요소를 참조할 때에는 대괄호`[]` 표기법을 사용한다. 대괄호 안에는 인덱스가 와야 한다.
- 배열 요소의 추가와 갱신
    - 배열에도 요소를 동적으로 추가할 수 있다. 만약 현재 배열의 length 프로퍼티 값보다 큰 인덱스로 새로운 요소를 추가하면 `희소 배열`이 된다.
    
    ```jsx
    const arr = [0];
    
    arr[3] = 3;
    
    console.log(arr); //[0, undefined, undefined, 3]
    console.log(arr.length); //4
    ```
    
    - 인덱스는 요소의 위치를 나타내므로 반드시 0 이상의 정수(또는 정수 형태의 문자열)를 사용해야 한다.  만약 정수 이외의 값을 인덱스처럼 사용하면 요소가 생성되는 것이 아니라 프로퍼티가 생성된다.
        
        ```jsx
        const arr = [];
        
        arr[0] = 1;
        arr['1'] = 2;
        
        //프로퍼티 추가
        arr['foo'] = 3;
        arr.bar = 4;
        arr[1.1]= 5;
        arr[-1] = 6;
        
        console.log(arr); //[1, 2]
        console.log(arr.length); //2
        ```
        
- 배열 요소의 삭제
    - `delete 연산자` 사용 할 수 있으나, 희소 배열을 만들 수 있으므로 사용하지 않는 것이 좋다.
        
        ```jsx
        delete arr[1];
        ```
        
    - 희소 배열을 만들지 않으면서 배열의 특정 요소를 완전히 삭제하려면 `Array.prototype.splice` 메서드를 사용한다.
        - Array.prototype.splice(`삭제를 시작할 인덱스`, `삭제할 요소 수`)
        
        ```jsx
        const arr = [1,2,3];
        arr.splice(1, 1);
        console.log(arr); //[1, 3]
        ```
        
- 배열 메서드 : 가급적 원본 배열을 직접 변경하지 않은 메서드를 사용하는 편이 좋다.
    - Array.`isArray` : 전달된 인수가 배열이면 true, 아니며 false를 반환한다.
        
        ```jsx
        console.log(Array.
        isArray([1,2])); //true
        ```
        
    - Array.prototype.`indexOf` : 원본 배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환한다. 원본 배열에 인수로 전달한 요소와 중복되는 요소가 여러 개 있다면 첫 번째로 검색된 요소의 인덱스를 반환한다. 원본 배열에 인수로 전달한 요소가 존재하지 않으면 -1을 반환한다.
        
        ```jsx
        const arr = [1, 2, 2, 3];
        
        console.log(arr.indexOf(2)); //1
        console.log(arr.indexOf(4)); //-1
        
        //두 번째 인수는 검색을 시작할 인덱스다. 두 번째 인수를 생략하면 처음부터 검색한다.
        console.log(arr.indexOf(2,2)); //2
        ```
        
    - Array.prototype.`push` : push 메서드는 인수로 전달받은 모든 값을 원본 배열의 마지막 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다. 원본 배열을 직접 변경한다.
        
        ```jsx
        const arr = [1, 2];
        let result = arr.push(3, 4);
        console.log(result); //4
        console.log(arr); //[1, 2, 3, 4]
        ```
        
        - (대안1) 성능이 좋지 않으므로, length 프로퍼티를 사용하여 배열의 마지막에 요소를 직접 추가할 수도 있다.
            
            ```jsx
            const arr = [1, 2];
            arr[arr.length] = 3;
            console.log(arr); //[1, 2, 3]
            ```
            
        - (대안2) ES6의 스프레드 문법을 사용하면 원본 배열을 변경하는 부수 효과가 없어서 좋다.
            
            ```jsx
            const arr = [1, 2];
            const newArr = [...arr, 3, 4]
            console.log(newArr); //[1, 2, 3, 4]
            ```
            
    - Array.prototype.`pop` : 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다. 원본 배열이 빈 배열이면 undefined를 반환한다. 원본 배열을 직접 변경한다.
        
        ```jsx
        const arr = [1, 2];
        let result = arr.pop();
        console.log(result); //2
        console.log(arr) //[1]
        ```
        
    - Array.prototype.`unshift` :  인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다. 원본 배열을 직접 변경한다. 이보다는 ES6의 스프레드 문법을 사용하는 편이 좋다.
        
        ```jsx
        const arr = [1, 2];
        let result = arr.unshift(3,4);
        console.log(result); //4
        console.log(arr) //[3,4,1,2]
        ```
        
    - Array.prototype.`shift` : 원본 배열에서 첫 번째 요소를 제거하고 제거한 요소를 반환한다.
        
        ```jsx
        const arr = [1, 2];
        let result = arr.shift();
        console.log(result); //1
        console.log(arr) //[2]
        ```
        
    - Array.prototype.`concat` : 인수로 전달된 값들을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환한다. 원본 배열은 변경되지 않는다.
        
        ```jsx
        const arr1 = [1, 2];
        const arr2 = [3, 4];
        let result = arr1.concat(arr2);
        console.log(result); //[1, 2, 3, 4]
        console.log(arr1); //[1, 2]
        ```
        
        - **push/unshift 메서드와 concat 메서드를 사용하는 대신 ES6의 스프레드 문법을 일관성 있게 사용하는 것을 권장한다.**
    - Array.prototype`.splice` : 원본 배열의 중간에 요소를 추가하거나 중간에 있는 요소를 제거하는 경우 splice 메서드를 사용한다. 3개의 메개변수가 있으며 원본 배열을 직접 변경한다.
        - Array.prototype.splice(`start`, `deleteCount`, `items`...)
            - start : 원본 배열의 요소를 제거하기 시작할 인덱스
            - deleteCount : 원본 배열의 요소를 제거하기 시작할 인덱스인 start부터 제거할 요소의 개수(옵션)
            - items : 제거한 위치에 삽입할 요소들의 목록이며, 생략할 경우 원본 배열에서 요소들을 제거하기만 한다.(옵션)
        
        ```jsx
        const arr = [1, 2, 3, 4];
        
        //원본 배열의 인덱스 1부터 2개의 요소를 제거하고 그 자리에 새로운 요소 20, 30을 삽입한다.
        const result = arr.splice(1, 2, 20, 30);
        
        //제거한 요소가 배열로 반환된다.
        console.log(result); //[2, 3]
        
        //원본 배열을 직접 변경한다.
        console.log(arr); //[1, 20, 30, 4]
        ```
        
    - Array.prototype.`slice` : slice 메서드는 인수로 전달된 범위의 요소들을 `복사`하여 배열로 반환한다. 원본 배열은 변경되지 않는다.
        - Array.prototype.slice(`start`, `end`)
            - start : 복사를 시작할 인덱스이며, 음수인 경우 배열의 끝에서의 인덱스를 나타낸다.
            - end : 복사를 종료할 인덱스이며, 이 인덱스에 해당하는 요소는 복사되지 않는다. 생략 가능하며 기본값은 length 프로퍼티 값이다.
            
            ```jsx
            const arr = [1, 2, 3, 4];
            
            console.log(arr.slice(1,2)); //[2] : 1 인덱스부터 2 인덱스 전까지 
            console.log(arr.slice(-3)); //[2, 3, 4] :  뒤에서 3개 같은 느낌
            ```
            
    - Array.prototype.`join` : 원본 배열의 모든 요소를 문자열로 변환한 후, 인수로 전달받은 문자열, 즉 구분자로 연결한 문자열을 반환한다. 구분자는 생략 가능하며 기본 구분자는 콤마(',')다.
        
        ```jsx
         const arr = [1,2,3,4];
        
        console.log(arr.join()); //"1,2,3,4"
        console.log(arr.join('')); //"1234"
        console.log(arr.join(':')); //"1:2:3:4"
        ```
        
    - Array.prototype.`reverse` : 원본 배열의 순서를 반대로 뒤집어서 값을 반환한다. 원본 배열이 변경된다.
        
        ```jsx
        const arr = [1,2,3,4];
        const result = arr.reverse();
        console.log(arr); //[4, 3, 2, 1]
        console.log(result); //[4, 3, 2, 1]
        ```
        
    - Array.prototype.`fill` : 인수로 전달받은 값을 배열의 처음부터 끝까지 요소로 채운다. 원본 배열이 변경된다.
        
        ```jsx
        const arr = [1,2,3,4];
        arr.fill(0, 1, 3);
        console.log(arr); //[1, 0, 0, 4]
        ```
        
    - Array.prototype.`includes` : 배열 내에 특정 요소가 포함되어 있는지 확인하여 true 또는 false를 반환한다.
        
        ```jsx
        const arr = [1,2,3,4, NaN,6];
        console.log(arr.includes(2)); //true
        console.log(arr.includes(5)); //false
        console.log(arr.includes(NaN)); //true
        ```
        
    - Array.prototype.`flat` : 인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화한다. 인수를 생략할 경우 기본값은 1이다.  인수로 Infinity를 전달하면 중첩 배열 모두를 평탄화한다.
        
        ```jsx
        console.log([1, [2, [3, 4], 5]].flat());  //[1, 2, [3, 4], 5]
        console.log([1, [2, [3, 4], 5]].flat(Infinity)); //[1, 2, 3, 4, 5]
        ```
        
- 배열 고차 함수 : 고차 함수는 함수를 인수로 전달받거나 함수를 반환하는 함수를 말한다.  함수형 프로그래밍에 중요하다.
    - Array.prototype.`sort` : 배열의 요소를 정렬한다. 기본적으로 오름차순으로 정렬한다.
        
        ```jsx
        const fruits = ['Banana', 'Orange', 'Apple'];
        fruits.sort();
        console.log(fruits); //["Apple", "Banana", "Orange"]
        ```
        
        내림차순으로 정렬하려면 sort 메서드 사용 후 reverse 메서드를 사용해야 한다.
        
        ```jsx
        const fruits = ['Banana', 'Orange', 'Apple'];
        fruits.sort();
        fruits.reverse();
        console.log(fruits); //["Orange", "Banana", "Apple"]
        ```
        
    - Array.prototype.`forEach` : for 문을 대체할 수 있는 고차 함수이다. 반복문을 추상화한 고차 함수로서 내부에서 반복문을 통해 자신을 호출한 배열을 순회하면서 수행해야 할 처리를 콜백 함수로 전달받아 반복 호출한다.  undefined를 반환한다.
        - 매개변수 3개(요소값, 인덱스, this)
        
        ```jsx
        const numbers = [1, 2, 3];
        const pows = [];
        
        numbers.forEach(number => pows.push(number ** 2));
        console.log(pows); //[1, 4, 9]
        ```
        
        ```jsx
        const numbers = [1, 2, 3];
        
        //forEach 메서드는 원본 배열을 변경하지 않지만 콜백 함수를 통해 원본 배열을 변경할 수는 있다.
        // 콜백 함수의 세 번째 매개변수 arr은 원본 배열 numbers를 가리킨다.
        //따라서 콜백 함수의 세 번째 매개변수 arr을 직접 변경하면 원본 배열 numbers가 변경된다.
        numbers.forEach((item, index, arr) => { arr[index] = item **2;});
        console.log(numbers); //[1, 4, 9]
        ```
        
    - Array.prototype.`map`  : 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다. 콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다. 원본 배열은 변경되지 않는다. forEach와 달리 콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다.
        - 매개변수 3개(요소값, 인덱스, this)
        
        ```jsx
        const numbers = [1, 4, 9];
        
        const roots = numbers.map(item => Math.sqrt(item));
        console.log(roots); //[1, 2, 3]
        ```
        
    - Array.prototype.`filter` : 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다. 콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열을 반환한다. 원본 배열은 변경되지 않는다.
        - 매개변수 3개(요소값, 인덱스, this)
        
        ```jsx
        const numbers = [1, 2, 3, 4, 5];
        
        const odds = numbers.filter(item => item % 2); //1은 true
        console.log(odds); //[1, 3, 5]
        ```
        
    - Array.prototype.`reduce` : 자신을 호출한 배열을 모든 요소를 순회하며 인수로 전달받은 콜백 함수를 반복 호출한다. 콜백 함수의 반환값을 다음 순회 시에 콜백 함수의 첫번째 인수로 전달하면서 콜백 함수를 호출하여 `하나의 결과값`을 만들어 반환한다. 원본 배열은 변경되지 않는다.
        - 첫 번째 인수 : `콜백 함수(4개의 인수)`
            - 1. 초기값 또는 콜백 함수의 이전 반환값  `accumulator`
            - 2. reduce 메서드를 호출한 배열의 요소값  `currentValue`
            - 3. 인덱스  `index` (옵션)
            - 4. reduce 메서드를 호출한 배열 자체(this)  `array` (옵션)
        - 두 번째 인수 : `초기값` (옵션이므로 생략 가능, 그러나 초기값 전달하는 것이 안전)
        
        ```jsx
        const sum = [1,2,3,4].reduce((accumulator, currentValue, index, array) => accumulator + currentValue, 0);
        console.log(sum); //10
        ```
        
    - Array.prototype.`some` : 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다. 이때 콜백 함수의 반환값이 단 한번이라도 참이면 true, 모두 거짓이라면 false를 반환한다. 호출 배열이 빈 배열이면 false 반환한다.
        
        ```jsx
        console.log([5, 10, 15].some(item => item >10)); //true
        console.log([5, 10, 15].some(item => item <0)); //false
        ```
        
    - Array.prototype.`every` : 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다. 이때 콜백 함수의 반환값이 모두 참이면 true, 단 한 번이라도 거짓이면 false를 반환한다. 호출 배열이 빈 배열이면 true를 반환한다.
        
        ```jsx
        console.log([5, 10, 15].every(item => item >3)); //true
        console.log([5, 10, 15].every(item => item >10)); //false
        ```
        
    - Array.prototype.`find` : 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 `첫 번째 요소`를 반환한다.  콜백함수의 반환값이 true인 요소가 존재하지 않는다면 `undefined`를 반환한다.
        
        ```jsx
        const users= [
          {id:1, name: "A"},
          {id:2, name: "B"},
          {id:2, name: "C"},
          {id:3, name: "D"}
        ];
        
        console.log(users.find(user=>user.id === 2));  //[object Object] { id: 2, name: "B"}
        ```
        
    - Array.prototype.`findIndex` : 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 첫 번째 요소의 `인덱스`를 반환한다.  콜백함수의 반환값이 true인 요소가 존재하지 않는다면 `-1`를 반환한다.
        
        ```jsx
        const users= [
          {id:1, name: "A"},
          {id:2, name: "B"},
          {id:2, name: "C"},
          {id:3, name: "D"}
        ];
        
        console.log(users.findIndex(user=>user.id === 2));  //1
        
        ```
        
    - Array.prototype.`flatmap` : map 메서드를 통해 생성된 새로운 배열을 1단계 평탄화한다. (map메서드 + flat 메서드)
        
        ```jsx
        const arr = ['hello','world'];
        console.log(arr.map(x=> x.split('')).flat());
        console.log(arr.flatMap(x=> x.split('')));
        ```
        
    

## Number

- Number 프로퍼티
    - Number.EPSILON
    - Number.MAX_VALUE
    - Number.MIN_VALUE
    - Number.MAX_SAFE_INTEGER
    - Number.MIN_SAFE_INTEGER
    - Number.POSITIVE_INFINITY
    - Number.NEGATIVE_INFINITY
    - Number.NaN
- Number 메서드
    - Number.isFinite
    - Number.isInteger
    - Number.isNaN
    - Number.isSafeInteger
    - Number.prototype.toExponential
    - Number.prototype.toFixed : 반올림
    - Number.prototype.toPrecision : 반올림
    - Number.prototype.toString

# Math

Math는 생성자 함수가 아니므로, 정적 프로퍼티와 정적 메서드만 제공한다.

- Math 프로퍼티
    - Math.PI
- Math 메서드
    - Math.abs
    - Math.round : 인수로 전달된 숫자의 소수점 이하를 `반올림`한 정수를 반환
    - Math.ceil : 인수로 전달된 숫자의 소수점 이하를 `올림`한 정수를 반환
    - Math.floor : 인수로 전달된 숫자의 소수점 이하를 `내림`한 정수를 반환
    - Math.sqrt : 제곱근
    - Math.random : 0에서 1미만의 임의의 난수(0은 포함되지만 1은 포함 안됨)
    - Math.pow : 첫 번째 인수를 밑으로, 두 번째 인수를 지수로 거듭제곱한 결과를 반환한다
    - Math.max : 전달받은 인수 중 가장 큰 수 반환
    - Math.min : 전달받은 인수 중 가장 작은 수 반환

## Date

- 현재 날짜와 시간은 자바스크립트 코드가 실행된 시스템의 시계에 의해 결정된다.
- Date 생성자 함수
    - new Date() : 현재 날짜와 시간을 가지는 Date 객체 반환
    - new Date(밀리세컨즈) : 밀리초를 인수로 전달하면 `1970년 1월 1일 00:00:00(UTC)`을 기점으로 인수로 전달된 밀리초만큼 경과한 날짜와 시간을 나타내는 Date 객체 반환
    - new Date(dateString)
    - new Date(year,month,day,hour,minute,second,millisecond)
- Date 메서드
    - Date.now()
        - `1970년 1월 1일 00:00:00(UTC)` 을 기점으로 현재 시간까지 경과한 밀리초를 숫자로 반환
    - Date.parse(지정시간)
        - `1970년 1월 1일 00:00:00(UTC)`을 기점으로 인수로 전달된 지정 시간까지의 밀리초를 숫자로 변환
    - getFullYear
    - setFullYear
    - getMonth : 1월은 0, 12월은 11
    - setMonth :
    - getDate : 날짜(1~31) 반환
    - setDate
    - getDay : 요일(일 0, 월 1, ~ 토 6) 반환
    - getHours : 시간(0~23) 반환
    - setHours
    - getMinutes : 분(0~59) 반환
    - setMinutes
    - getSeconds : 초(0~59) 반환
    - setSeconds
    - getMilliseconds : 밀리초(0~999) 반환
    - setMilliseconds
    - getTime :  `1970년 1월 1일 00:00:00(UTC)` 을 기점으로 Date 객체의 시간까지 경과된 밀리초를 반환
    - setTime
    - getTimezoneOffset : UTC와 Date 객체에 지정된 로컬 시간과의 차이를 분 단위로 반환한다. (UST = KST - 9h)
    - toDateString : 문자열로 Date 객체의 날짜 반환
    - toTimeString : 문자열로 Date 객체의 시간 반환
    - toISOString : ISO 8601 형식으로 Date객체의 날짜와 시간 표현 문자열을 반환
    - toLocaleString : 인수로 전달한 로캘을 기준으로 Date 객체의 날짜와 시간을 표현한 문자열 반환
    - toLocaleTimeString : 인수로 전달한 로캘을 기준으로 Date 객체의 시간을 표현한 문자열 반환

## RegExp

- 정규 표현식이란?
    - 일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어다. 무낮열을 대상으로 패턴 매칭 기능을 제공한다.
- 정규 표현식의 생성
    - 정규 표현식 리터럴
    
    ![regular_expression.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9f0d904b-2ed1-4e6b-aebe-e9f12f6f79d9/regular_expression.png)
    
    ```jsx
    const target = 'Is this all there is?';
    
    const regexp = /is/i;
    //위 코드는 아래 코드와 동일
    //const regexp = new RegExp(/all/i); 
    
    console.log(regexp.test(target)); //true
    ```
    
- RegExp 메서드
    - RegExp.prototype.exec : 매칭 결과를 배열로 반환
    - RegExp.prototype.test : 매칭 결과를 불리언 값으로 반환
    - String.prototype.match : 매칭 결과를 배열로 반환
        
        ```jsx
        const target = 'Is this all there is?';
        
        const regexp = /is/i;
        
        console.log(regexp.exec(target)); //["is"]
        console.log(target.match(regexp)); //["is"]
        ```
        
- 플래그 : 정규 표현식의 검색 방식을 설정하기 위해 사용한다. 하나 이상의 플래그를 동시에 설정할 수도 있다.  문자열에 패턴 검색 매칭 대상이 1개 이상 존재해도 첫 번째 매칭한 대상만 검색하고 종료한다.
    - i : 대소문자를 구별하지 않고 패턴을 검색한다(ignore case)
    - g : 대상 문자열 내에서 패턴과 일치하는 모든 문자열을 전역 검색한다(Global)
    - m : 문자열의 행이 바뀌더라도 패턴 검색을 계속한다(Multi line)
    
    ```jsx
    const target = 'Is this all there is?';
    
    console.log(target.match(/is/)); //["is"]
    console.log(target.match(/is/i)); //["Is"]
    console.log(target.match(/is/g)); //["is", "is"]
    console.log(target.match(/is/ig));  //["Is", "is", "is"]
    ```
    
- 패턴
    - 문자열 검색
    - 임의의 문자열 검색 : `.`은 임의의 문자 한 개를 의미한다.
        
        ```jsx
        const target = 'Is this all there is?';
        
        const regExp = /.../g;
        console.log(target.match(regExp)); //["Is ", "thi", "s a", "ll ", "the", "re ", "is?"]
        ```
        
    - 반복 검색 : `{m,n}` 은 앞선 패턴이 최소 m번, 최대 n번 반복되는 문자열을 의미한다. (콤마 뒤에 공백이 없어야 함) `{n} = {n,n}`은 앞선 패턴이 n번 반복되는 문자열을 의미한다. `{m,}`은 앞선 패턴이 최소 m번 이상 반복되는 문자열을 의미한다.
        
        ```jsx
        const target = 'A AA B BB Aa Bb AAA';
        
        const regExp = /A{1,2}/g;
        console.log(target.match(regExp)); //["A", "AA", "A", "AA", "A"]
        ```
        
    - OR 검색
        
        ```jsx
        const target = 'A AA B BB Aa Bb AAA';
        //A 또는 B를 전역 검색한다.
        const regExp = /A|B/g;
        console.log(target.match(regExp)); //["A", "A", "A", "B", "B", "B", "A", "B", "A", "A", "A"]
        ```
        
        - 분해되지 않은 단어 레벨로 검색하기 위해서는 `+` 를 함께 사용한다.
        - `[ ]` 내의 문자는 or로 동작한다.
        - 범위를 지정하려면 `[ ]` 내에 `-`를 사용한다.
        - `[\d]`는 숫자를 의미하며 `[0-9]`와 같다.
        - `[\D]`는 문자를 의미한다.
        - `[\w]`는 알파벳, 숫자, 언더스코어를 의미하며, `[A-Za-z0-9_]`와 같다
        - `[\W]`는 문자를 의미한다.
    - NOT 검색
        - [ ] 내의 `^`는 not의 의미를 갖는다. `[^0-9]`는 숫자를 제외한 문자를 의미한다.
    - 시작 위치로 검색
        - [ ] 밖의 `^`는 문자열의 시작을 의미한다.
        
        ```jsx
        const target = 'https://jsbin.com/';
        //'https'로 시작하는지 검색한다
        const regExp = /^https/;
        console.log(regExp.test(target)); //true
        ```
        
    - 마지막 위치로 검색
        - `$`는 문자열의 마지막을 의미한다.
        
        ```jsx
        const target = 'https://jsbin.com';
        //'com'로 끝나는지 검색한다
        const regExp = /com$/;
        console.log(regExp.test(target)); //true
        ```
        

## String

- String 메서드
    - indexOf
    - search
    - includes
    - startsWith
    - endsWith
    - charAt
    - substring
    - slice
    - toUpperCase
    - toLowerCase
    - trim
    - repeat
    - repalce
    - split

## 7번째 데이터 타입 Symbol

- 심벌이란 : ES6에서 도입된 7번째 데이터 타입으로 변경 불가능한 원시 타입의 값이다. 심벌 값은 다른 값과 중복되지 않는 유일무이한 값이다. 따라서 주로 이름의 충돌 위험이 없는 유일한 프로퍼티 키를 만들기 위해 사용한다.
- 심벌 값의 생성
    - Symbol 함수 : 생성된 심벌 값은 외부로 노출되지 않아 확인할 수 없고, 다른 값과 절대 중복되지 않는 유일무이한 값이다. new 연산자를 붙이지 않는다.
    
    ```jsx
    const mySymbol1 = Symbol();
    const mySymbol2 = Symbol();
    
    console.log(mySymbol1) //[object Symbol] { ... }
    console.log(mySymbol1 === mySymbol2) //false
    ```
    
    - Symbol.for 메서드는 인수로 전달받은 문자열을 키로 사용하여 키와 심벌 값의 쌍들이 저장되어 있는 전역 심벌 레지스트리에서 해당 키와 일치하는 심벌 값을 검색하고, 없으면 새 심벌 값을 `생성하고`, 있으면 해당 심벌 `값`을 `반환한다`.
    - Symbol.keyFor 메서드를 사용하면 전역 심벌 레지스트리에 저장된 심벌 값의 `키`를 `추출`할 수 있다.
    
    ```jsx
    const mySymbol = Symbol('key1');
    const s1 = Symbol.for('key1');
    const s2 = Symbol.for('key1');
    console.log(s2 === s1) //true
    console.log(Symbol.keyFor(s1)); //"key1"
    ```
    

## 이터러블

- 이터레이션 프로토콜 : ES6에서 도입된 이터레이션 프로토콜은 순회 가능한 데이터 컬렉션을 만들기 위해 미리 약속한 규칙이다.

## 스프레드 문법

ES6에서 도입된 스프레드 문법 `...`은 하나로 뭉쳐 있는 여러 값들의 집합을 펼쳐서 개별적인 값들의 목록으로 만든다.

- 스프레드 문법의 결과는 값이 아니고 값들의 목록이다. 스프레드 문법의 결과는 변수에 할당할 수 없다. 함수 호출문의 인수 목록, 배열 리터럴의 요소 목록, 객체 리터럴의 프로퍼티 목록에서만 사용할 수 있다.
- 함수 호출문의 인수 목록에서 사용하는 경우
    
    ```jsx
    const arr = [1,2,3];
    const max = Math.max(...arr);
    console.log(max); //3
    ```
    
    - `스프레드 문법`은 `Rest 파라미터` 와 형태가 동일하여 혼동할 수 있으나 서로 반대의 개념이므로 주의할 필요가 있다.
        - `Rest 파라미터`는 함수에 전달된 인수들의 목록을 배열로 전달받기 위해 매개변수 이름 앞에 `...`을 붙이는 것이다.
        - `스프레드 문법`은 여러 개의 값이 하나로 뭉쳐 있는 배열과 같은 이터러블을 펼쳐서 개별적인 값들의 목록을 만드는 것이다.
- 배열 리터럴 내부에서 사용하는 경우
    - concat처럼
        
        ```jsx
        const arr = [...[1,2], ...[3,4]];
        console.log(arr); //[1, 2, 3, 4]
        ```
        
    - splice처럼
        
        ```jsx
        const arr1 = [1, 4];
        const arr2 = [2, 3];
        
        arr1.splice(1, 0, ...arr2);
        console.log(arr1); //[1, 2, 3, 4]
        ```
        
    - slice 처럼
        
        ```jsx
        const origin = [1,2];
        const copy = [...origin];
        
        console.log(copy); //[1, 2]
        console.log(origin === copy); //false
        // 얕은 복사하여 새로운 복사본을 생성한다
        ```
        
    - 이터러블을 배열로 변환
        
        ```jsx
        function sum() {
          return [...arguments].reduce((pre, cur) => pre + cur, 0);
        }
        
        console.log(sum(1, 2, 3));//6
        ```
        
        - (참고)Rest 파라미터 사용
            
            ```jsx
            const sum = (...args) => args.reduce((pre, cur) => pre + cur, 0);
            console.log(sum(1,2,3)); //6
            ```
            
        - 이터러블이 아닌 유사 배열 객체를 배열로 변경하려면 ES6에서 도입된 `Array.from` 메서드 사용한다. 이를 사용하면 유사 배열 객체 또는 이터러블을 인수로 받아 배열로 변환하여 반환한다.
- 객체 리터럴 내부에서 사용하는 경우
    - Object.assign 메서드를 대체할 수 있다.
    
    ```jsx
    // 객체 복사(얕은 복사)
    const obj = {x:1, y:2};
    const copy = {...obj};
    console.log(copy); //{x:1, y:2}
    console.log(obj === copy); //false 
    
    // 객체 병합, 프로퍼티가 중복되는 경우 뒤에 위치한 프로퍼티가 우선권을 갖는다.
    const merged = {x:1, y:2, ...{y:3, z:4}};
    console.log(merged); //{x:1, y:3, z:4}
    ```
    

## 디스트럭처링 할당

Destructuring assignment(구조 분해 할당)은 구조화된 배열과 같은 이터러블 또는 객체를 destructuring(비구조화, 구조 파괴) 하여 1개 이상의 변수에 개별적으로 할당하는 것을 말한다.  

- 배열 디스트럭처링 할당
    - 배열 디스트럭처링 할당  대상(할당문의 우변)은 이터러블이어야 하며, 할당 기준은 배열의 인덱스다(순서대로 할당된다).
        
        ```jsx
        const arr = [1,2,3];
        const [one, two, three] = arr;
        console.log(one, two, three); // 1 2 3
        ```
        
    - 변수에 기본값을 설정할 수 있다.
        
        ```jsx
        const arr = [1,2,3];
        const [one, two, three, four=4 ] = arr;
        console.log(one, two, three, four); // 1 2 3 4
        ```
        
    - Rest 요소를 사용할 수 있으며, Rest요소는 반드시 마지막에 위치해야 한다.
        
        ```jsx
        const arr = [1,2,3];
        const [one, ...other] = arr;
        console.log(one, other); // 1 [2, 3]
        ```
        
- 객체 디스트럭처링 할당
    - 할당의 대상(할당문의 우변)은 객체이어야 하며, 할당 기준은 프로퍼티 키다. 순서는 의미가 없다. 선언된 변수 이름과 프로퍼티 키가 일치하면 할당된다. 객체 디스트러처링 할당은 프로퍼티 키로 필요한 프로퍼티 값만 추출하여 변수에 할당하고 싶을 때 유용하다.
        
        ```jsx
        const user = { firstName : 'Marco', lastName : 'Jang'};
        
        const { lastName, firstName} = user;
        console.log(firstName, lastName); //Marco Jang
        ```
        
        - 객체의 프로퍼티 키와 다른 변수 이름으로 프로퍼티 값을 할당받으려면 다음과 같이 변수를 선언한다.
            
            ```jsx
            const user = { firstName : 'Marco', lastName : 'Jang'};
            
            const { lastName : ln, firstName: fn} = user;
            console.log(fn, ln); //Marco Jang
            ```
            
        - 변수에 기본값을 설정할 수 있다.
        - 배열의 요소가 객체인 경우 배열 디스트럭처링 할당과 객체 디스트럭처링 할당을 혼용할 수 있다.
        - 중첩 객체
            
            ```jsx
            const user = {
              name: 'Marco',
              address: {
                zipcode : '324234',
                city: 'Seoul'
              }
            };
            
            const {address: {city}} = user;
            console.log(city); //Seoul
            ```
            
        - Rest 프로퍼티 `...` 를 사용할 수 있고 반드시 마지막에 위치해야 한다.
