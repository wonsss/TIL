# [책 요약] YOU DON'T KNOW JS - this와 객체 프로토타입, 비동기와 성능

# 1. this라나 뭐라나

## 1.1 this를 왜?

- idetinfy()와 speak() 두 함수는 객체별로 따로따로 함수를 작성할 필요 없이  다중 콘텍스트 객체인 me와 you 모두에서 재사용할 수 있다. 암시적인 객체 레퍼런스를 '함께 넘기는' this 체계가 API 설계상 조금 더 깔끔하고 명확하며 재사용하기 쉽다. 사용 패턴이 복잡해질수록 보통 명시적인 인자로 콘텍스트를 넘기는 방법(매개변수)이 ths 콘텍스트를 사용하는 것보다 코드가 더 지저분해진다.
- 여러 함수가 적절한 콘텍스트 객체를 자동 참조하는 구조가 편리하다.

```jsx
function identify() {
  return this.name.toUpperCase();
}

function speak() {
  const greeting = `Hello, I'm ${identify.call(this)}`;
  console.log(greeting);
}

const me = {
  name: 'Marco',
};

const you = {
  name: 'Reader',
};

identify.call(me);
identify.call(you);
speak.call(me);
speak.call(you);
```

## 1.2 헷갈리는 것들

### 1.2.1 자기 자신

- this가 함수 그 자체를 가리킨다는 것은 오해이다.
    - 자바스크립트에서 함수는 this로 자기 참조를 할 수가 없다.
    - 함수가 내부에서 자신을 참조할 때 일반적으로 this만으로는 부족하며 렉시컬 식별자(Lexical Identifier, 변수)를 거쳐 함수 객체를 참조한다.
        - 기명함수는 함수명 자체가 내부에서 자신을 가리키는 레퍼런스로 쓰인다.
        - 하지만 익명함수는 함수 자신을 참조할 방법이 마땅치 않다.
        
        ```jsx
        function foo(num) {
          console.log('foo: ' + num);
        
          this.count++; // this.count에서 this는 함수 객체를 바라보는 것이 아니며, 전역을 바라본다.
        }
        
        foo.count = 0; // foo 함수 객체에 count 프로퍼티가 추가된다.
        
        for (let i = 0; i < 10; i++) {
          if (i > 5) {
            foo(i);
          }
        }
        
        console.log(foo.count); // 0
        ```
        
        ```jsx
        function foo(num) {
          console.log('foo: ' + num);
        
          foo.count++; // this 없이 함수 객체 레퍼런스로 foo 식별자를 대신 사용할 수 있다.
        }
        
        foo.count = 0;
        
        for (let i = 0; i < 10; i++) {
          if (i > 5) {
            foo(i);
          }
        }
        
        console.log(foo.count); // 4
        ```
        
        ```jsx
        function foo(num) {
          console.log('foo: ' + num);
        
          this.count++; // this를 사용하면서
        }
        
        foo.count = 0;
        
        for (let i = 0; i < 10; i++) {
          if (i > 5) {
            foo.call(foo, i); // foo 함수 내부에서 this가 foo함수 객체를 직접 가리키도록 강제한다.
          }
        }
        
        console.log(foo.count); // 4
        ```
        

### 1.2.2 자신의 스코프

- 
- this가 바로 함수의 스코프를 가리킨다는 말도 오해다.
    - 분명한 것은 `this`는 어떤 식으로도 `함수의 렉시컬 스코프를 참조하지 않는다`는 사실이다.
        - 내부적으로 `스코프`는 별개의 식별자가 달린 프로퍼티로 구성된 `객체`의 일종이나 `스코프 '객체'`는 자바스크립트 구현체인 '엔진'의 `내부 부품`이기 때문에 `일반 자바스크립트 코드로는 접근하지 못한다`.
    - 렉시컬 스코프 안에 있는 뭔가를 this 레퍼런스로 참조할 수 없다.

## 1.3 this는 무엇인가?

- this는 작성 시점이 아닌 `런타임 시점(호출)` 에 `바인딩` 되며, `함수 호출 당시 상황`에 따라 `콘텍스트`가 결정된다.
    - 즉, 함수 선언 위치와 상관없이 this 바인딩은 오로지 어떻게 함수를 호출했느냐에 따라 정해진다.
- 어떤 함수를 호출하면 `활성화 레코드`(=실행 콘텍스트) 가 만들어진다.
    - 여기엔 함수가 호출된 근원(콜스택)과 호출 방법, 전달된 인자 등의 정보가 담겨 있다.
        - this 레퍼런스는 그 중 하나로, 함수가 실행되는 동안 이용할 수 있다.

## 1.4. 정리하기

- this는 함수 자신을 가리키지 않는다.
- this는 함수의 렉시컬 스코프를 가리키는 레퍼런스가 아니다.
- this는 실제로 `함수 호출 시점`에 바인딩되며, 무엇을 가리킬지는 전적으로 `함수를 호출한 코드`에 달렸다.

# 2. this가 이런 거로군!

## 2.1 호출부

## 2.2 단지 규칙일 뿐

### 2.2.1 기본 바인딩

- 단독 함수 실행(standalone function invocation)에 관한 규칙
    - 나머지 규칙에 해당하지 않을 경우 적용되는 this의 기본 규칙이다.
        - 전역 스코프에 변수를 선언하면 변수명과 같은 이름의 전역 객체 프로퍼티가 생성된다.
        - 함수 호출부가 지극히 평범한 있는 그대로의 함수 레퍼런스로 함수 호출 시, 함수 내부의 this는 `기본 바인딩`이 적용되어 `전역 객체`를 참조한다.
            - 엄격 모드에서는 전역 객체가 기본 바인딩에서 제외되어, this가 undefined이다.
            - 미묘하지만 중요한 사실은 보통 this 바인딩 규칙은 오로지 호출부에 의해 좌우되지만 비엄격 모드에서는 함수의 본문을 실행하면 전역 객체만이 기본 바인딩의 유일한 대상이라는 점이다. 즉, 함수 호출부의 엄격 모드 여부는 상관없다.

```jsx
function foo() {
	console.log(this.a);
}

let a = 2; // 전역 스코프에 변수를 선언하면 변수명과 같은 이름의 전역 객체 프로퍼티가 생성된다.
foo(); // 2
```

### 2.2.2 암시적 바인딩

- 호출부에 콘텍스트 객체가 있는지, 즉 객체의 소유/포함 여부를 확인한다.

```jsx
function foo() {
	console.log(this.a);
}

var obj = {
	a: 2,
	foo: foo
}

obj.foo(); //2
```

- foo 호출 시점에 obj 객체 레퍼런스는 준비된 상태다. 함수 레퍼런스에 대한 콘텍스트 객체가 존재할 때 암시적 바인딩 규칙에 따르면 바로 이 콘텍스트가 객체를 함수 호출 시 this에 바인딩 된다.
    - 즉, 위 예제에서 foo() 호출 시 obj는 this이니 this.a는 obj.a가 된다.
- 객체 프로퍼티 참조가 체이닝된 형태라면 최상위/최하위 수준의 정보만 호출부와 연관된다.

```jsx
function foo() {
	console.log(this.a);
}

var obj2 = {
	a: 42,
	foo: foo
}

var obj1 = {
	a: 2,  // 중간 단계인 obj1.a 값 2는 무시된다.
	obj2: obj2
}

obj1.obj2.foo(); //42
```

- 암시적 소실
    
    ```jsx
    function foo() {
      console.log(this.a);
    }
    
    var obj = {
      a: 2,
      foo: foo,
    };
    
    var bar = obj.foo;
    var a = '엥 전역이네';
    bar(); // 'undefined'
    ```
    

### 2.2.3 명시적 바인딩

- 함수 레퍼런스 프로퍼티를 객체에 더하지 않고 어떤 객체를 this 바인딩에 이용하겠다는 의지를 코드에 명확히 밝힐 방도는 없을까?
    - call()과 apply() 메서드를 이용할 수 있다.
    - 두 메서드는 this에 바인딩할 객체를 첫째 인자로 받아 함수 호출 시 이 객체를 this로 세팅한다. this를 지정한 객체로 직접 바인딩하므로 이를 '명시적 바인딩'이라 한다.
    - foo.call()에서 명시적으로 바인딩하여 함수를 호출하므로 this는 반드시 obj가 된다.
    
    ```jsx
    function foo() {
      console.log(this.a);
    }
    
    var obj = {
      a: 2,
    };
    
    foo.call(obj); // 2
    ```
    
- 하드 바인딩
    - 명시적 바인딩을 약간 변형한 꼼수가 있다.
        - bar를 어떻게 호출하든 이 함수는 항상 obj를 바인당하게 하기 위해, bar 함수 내부에 foo.call(obj)로 foo를 호출하도록 하여, obj를 this에 강제로 바인딩하도록 하드 코딩한다.
        - 함수 바인딩으로 함수를 감싸는 형태의 코드는 다음과 같이 인자를 넘기고 반환 값을 돌려받는 창구가 필요할 때 주로 쓰인다.
        
        ```jsx
        function foo(something) {
          console.log(this.a, something);
          return this.a + something;
        }
        
        const obj = {
          a: 2,
        };
        
        const bar = function () {
          return foo.apply(obj, arguments);
        };
        
        const b = bar(3);
        console.log(b);
        ```
        
        ```jsx
        function foo(something) {
          console.log(this.a, something);
          return this.a + something;
        }
        
        const obj = {
          a: 2,
        };
        
        const bar = foo.bind(obj);
        
        const b = bar(3);
        console.log(b);
        ```
        
        - bind()는 주어진 this 콘텍스트로 원본 함수를 호출하도록 하드 코딩된 새 함수를 반환한다.

### 2.2.4 new 바인딩

- 자바스크립트에서 new는 의미상 클래스 지향적인 기능과 아무 상관이 없다.
- 자바스크립트에서 '생성자'는 앞에 new 연산자가 있을 때 호출되는 일반 함수에 불과하다.
    - 클래스에 붙은 것도 아니고 클래스 인스턴스화 기능도 없다.
    - 심지어 특별한 형태의 함수도 아니다.
    - 단지 new를 사용하여 호출할 때 자동으로 붙들려 실행되는 평범한 함수다.
- 함수 앞에 new를 붙여 생성자 호출을 하면 다음과 같은 일들이 저절로 일어난다.
    1. 새 객체가 툭 만들어진다.
    2. 새로 생성된 객체의 [[prototpye]]이 연결된다.
    3. 새로 생성된 객체는 해당 함수 호출 시 this로 바인딩된다.
    4. 이 함수가 자신의 또 다른 객체를 반환하지 않는 한 new와 함께 호출된 함수는 자동으로 새로 생성된 객체를 반환한다. 
    
    ```jsx
    function foo(a) {
      this.a = a;
    }
    const bar = new foo(2);
    console.log(bar.a);
    ```
    
    - 앞에 new를 붙여 foo()를 호출했고 새로 생성된 객체는 foo 호출 시 this에 바인딩된다. 따라서 결국 new는 함수 호출 시 this를 새 객체와 바인딩 하는 방법이며 이것이 'new 바인딩'이다.

## 2.3 모든 건 순서가 있는 법

- 우선순위
    1. 명시적 바인딩(하드 코딩)
    2. new 바인딩
    3. 암시적 바인딩
    4. 기본 바인딩
    
    ```jsx
    function foo(something) {
      this.a = something;
    }
    
    const obj1 = {};
    
    const bar = foo.bind(obj1);
    bar(2);
    console.log(obj1.a); // 2
    
    const baz = new bar(3);
    // new bar(3) 실행 후에도 obj1.a 값은 3으로 바뀌지 않고, 
    console.log(obj1.a); // 2
    // new 가 적용되므로 새로 만들어진 객체가 baz에 할당되고, baz.a값은 3이 된다.
    console.log(baz.a); // 3
    ```
    
    - 굳이 new로 하드 바인딩을 오버라이드하려는 이유는 뭘까? 기본적으로 this하드 바인딩은 무시하는 함수를 생성하여 함수 인자를 전부 또는 일부만 미리 세팅해야 할 때 유용하다. bind() 함수는 최초 this 바인딩 이후 전달된 인자를 원 함수의 기본 인자로 고정하는 역할을 한다.
    
    ```jsx
    function foo(p1, p2, p3) {
      this.val = p1 + p2 + p3;
    }
    
    const obj = {
      val: 'hi',
    };
    // this 하드 바인딩은 여기서 어차피 'new'호출 시 오버라이드된다.
    const bar = foo.bind(obj, 'p1');
    const baz = new bar('p2', 'p3');
    
    console.log(baz.val); //p1p2p3
    ```
    

### 2.3.1 this 확정 규칙

다음 항목을 순서대로 따져보고 그중 맞아떨어지는 최초 규칙을 적용한다.

1. new로 함수를 호출(new 바인딩)했는가? → 맞으면 새로 생성된 객체(`bar`)가 this다.
    
    ```jsx
    const bar = new foo();
    ```
    
2. call과 apply로 함수를 호출(명시적 바인딩), 이를테면 bind 하드 바인딩 내부에 숨겨진 형태로 호출됐는가? → 맞으면 명시적으로 지정된 객체(`obj2`)가 this다.
    
    ```jsx
    const bar = foo.call(obj2);
    ```
    
3. 함수를 콘텍스트(암시적 바인딩), 즉 객체를 소유 또는 포함하는 형태로 호출했는가? → 맞으면 바로 이 콘텍스트 객체(`obj1`)가 this다.
    
    ```jsx
    const bar = obj1.foo();
    ```
    
4. 그 외의 경우에 this는 기본값(엄격모드는 `undefined`, 비엄격 모드는 `전역 객체`)으로 세팅된다(기본바인딩).
    
    ```jsx
    const bar = foo();
    ```
    

## 2.4 바인딩 예외

### 2.4.1 this 무시

- call, apply, bind 메서드에 첫 번째 인자로 null 또는 undefined를 넘기면 this 바인딩이 무시되고 기본 바인딩 규칙(전역객체나 undefined 참조)이 적용된다.
    - 그런데 왜 null 같은 값으로 this 바인딩을 하려는 걸까?
        - apply()는 함수 호출 시 다수의 인자를 배열 값으로 죽 펼쳐 보내는 용도로 자주 쓰인다.
            - ES6부터는 spread operator를 이용해서 apply() 없이 인자를 배열 형태로 펼칠 수 있다. foo(...[1,2])는 foo(1,2)와 같다.
            
            ```jsx
            function foo(a, b) {
              console.log(`a: ${a}, b: ${b}`); 
            }
            
            // 인자들을 배열 형태로 죽 펼친다.
            foo.apply(null, [2, 3]); 
            // a:2, b:3
            ```
            
        - bind()도 유사한 방법으로 인자들(미리 세팅된 값들)을 커링하는 메서드로 많이 사용한다.
            
            ```jsx
            function foo(a, b) {
              console.log(`a: ${a}, b: ${b}`); 
            }
            
            // bind()로 커링한다
            const bar = foo.bind(null, 2);
            bar(3);
            // a:2, b:3
            ```
            
        - apply와 bind 모두 반드시 첫 번째 인자로 this 바인딩을 지정해야 한다. 하지만 this가 로직상 아무래도 좋다면 일종의 자리 끼움 값으로 null 정도의 값을 전달하는 편이 합리적이다.
            - 하지만 이와 같이 this 바인딩을 상관하지 않고 null을 애용하는 건 리스크가 있다. 마침 그 함수가 내부적으로 this를 참조하면 기본 바인딩이 적용되어 전역 변수를 참조하거나 변경하는 예기치 못한 일이 발생할 수 있기 때문이다.
- 더 안전한 this
    - 내용이 하나도 없으면서 전혀 위임되지 않은 객체(속칭 DMZ 객체) 정도가 필요하다.
        - this 바인딩을 신경 쓰지 않고 싶을 때마다 이러한 DMZ 객체를 전달하면, 받는 쪽에서 this를 어찌 사용하든지 어차피 대상은 빈 객체로 한정되므로 최소한 전역 객체를 건드리는 부작용은 방지할 수 있다.
        - 빈 객체를 만드는 간단한 방법은 Object.create(null)이다. 이는 객체 리터럴인 {}과 비슷하나 Object.prototype으로 위임하지 않으므로 {}보다 '더 텅 빈' 객체라고 볼 수 있다.
        
        ```jsx
        function foo(a, b) {
          console.log(`a: ${a}, b: ${b}`);
        }
        // DMZ 객체 생성
        const dmz = Object.create(null);
        // bind()로 커링한다
        const bar = foo.bind(dmz, 2);
        bar(3);
        // a:2, b:3
        ```
        

### 2.4.2 간접 레퍼런스

### 2.4.3 소프트 바인딩

## 2.5 어휘적 this

- 일반적인 함수는 지금까지 살펴본 4가지 규칙을 준수한다.
- 하지만 ES6부터 도입된 `화살표 함수` 는 이러한 규칙을 따르지 않는다.
    - `화살표 함수` 는 4가지 표준 규칙 대신 `에두른 스코프(Enclosing Scope)`를 보고 this를 알아서 바인딩한다.
    
    ```jsx
    var a = '1';
    
    function foo() {
      setTimeout(function () {
        console.log(this.a);
      }, 100);
    }
    const obj = {
      a: 2,
    };
    
    foo.call(obj); // 1
    ```
    
    ```jsx
    var a = '1';
    
    function foo() {
      setTimeout(() => {
        console.log(this.a);
      }, 100);
    }
    
    const obj = {
      a: 2,
    };
    
    foo.call(obj); // 2
    ```
    
    - 화살표 함수의 어휘적 바인딩은 절대로 오버라이드할 수 없다.
- 화살표 함수는 this를 확실히 보장하는 수단으로 bind()를 대체할 수 있고 겉보기에도 끌리는 구석이 있지만, 결과적으로 더 잘 알려진 렉시컬 스코프를 쓰겠다고 기존의 this 체계를 포기하는 형국이란 점을 간과하면 안 된다.
    - ES6 이전에도 화살표 함수의 기본 기능과 크게 다르지 않는, 많이 쓰이던 패턴이 있었다. 그것은 const self = this; 와 같이 this를 어휘적으로 포착하는 방법이다.
    - 화살표 함수나 self=this는 모두 bind() 대신 사용 가능한 좋은 해결책이지만, this를 제대로 이해하고 수용하기보단 골치 아픈 this에서 도망치려는 꼼수라고 할 수 있다.
- 어쨌거나 this 스타일의 코드를 작성할 경우, 어휘적 self = this든, 화살표 함수 꼼수든 다음 두 가지 중 하나만 선택하는 것이 좋다.

## 2.6 정리하기

- 함수 호출부를 식별한 후 다음 우선순위에 따라 적용한다
    1. new로 호출했다면 새로 생성된 객체로 바인딩된다.
    2. call이나 apply 또는 bind로 호출됐다면 주어진 객체로 바인딩된다.
    3. 호출의 주체인 콘텍스트 객체로 호출됐다면 바로 이 콘텍스트 객체로 바인딩된다.
    4. 기본 바인딩에서 엄격 모드는 undefined, 그 밖엔 전역 객체로 바인딩된다.
- this 바인딩을 안전하게 하려면 const dmz = Object.create(null) 처럼 DMZ 객체를 자리 끼움 값으로 바꿔 넣어 뜻하지 않은 부수 효과가 전역 객체에서 발생하지 않게 한다.
- ES6 화살표 함수는 표준 바인딩 규칙을 무시하고 렉시컬 스코프로 this를 바인딩한다. 즉, 에두른 함수 호출로부터 어떤 값이든 this 바인딩을 상속한다.

# 3. 객체

## 3.1 구문

- 객체는 선언적(리터럴) 형식과 생성자 형식, 두 가지로 정의한다
    - 리터럴 형식
        - 한 번의 선언으로 다수의 키/값 쌍을 프로퍼티로 추가할 수 있다.
        - 내장 객체 등 대부분 리터럴 형식을 사용한다.
        
        ```jsx
        const myObj = {
        	key: value
        }
        ```
        
    - 생성자 형식
        - 한 번에 한 프로퍼티만 추가할 수 있다.
        - 생성자 형식으로 객체를 생성하는 일은 매우 드물다.
        
        ```jsx
        const myObj = new Object();
        myObj.key = value;
        ```
        

## 3.2 타입

- 단순 원시 타입(string, number, boolean, null, undefined)은 객체가 아니다. 이 외 나머지는 거의 객체에 포함된다.
- `function` 은 객체의 하위 타입이다. 함수는 기본적으로 '일급 객체'이며, 여타의 일반 객체와 똑같이 취급된다.
- `배열` 역시 추가 기능이 구현된 객체의 일종이다. 다른 일반 객체보다 좀 더 조직적으로 데이터가 구성되는 특징이 있다.

### 3.2.1 내장 객체

- 내장 객체라는 객체 하위 타입도 있다.
    - String, Number, Boolean, Object, Function, Array, Date, RegExp, Error
- 이들은 진짜 타입처럼 보이는 데다 클래스처럼 느껴진다. 하지만 이들은 단지 `내장 함수`일 뿐 각각 생성자로 사용되어 주어진 하위 타입의 새 객체를 생성한다.

```jsx
// 객체 하위 타입을 확인한다
Object.prototype.toString.call(obj);
```

## 3.3 내용

- 객체는 특정한 위치에 저장된 모든 타입의 값, 즉 프로퍼티로 내용이 채워진다.
- 객체 프로퍼티명은 언제나 문자열이다. 문자열 이외의 다른 원시 값을 쓰면 우선 문자열로 변환된다.

### 3.3.1 계산된 프로퍼티명

객체 리터럴 선언 구문의 키 이름 부분에 해당 표현식을 넣고 [ ] 로 감싸면 된다.

```jsx
const prefix = 'foo';
const myObject = {
  [prefix + 'bar']: 'hello',
  [prefix + 'baz']: 'world',
};

console.log(myObject['foobar']); // hello
console.log(myObject['foobaz']); // world
```

### 3.3.2 프로퍼티 vs 메서드

- 자바스크립트에서 '함수'와 '메서드'란 말은 서로 바꿔 사용할 수 있다.
- 함수 표현식을 객체 리터럴의 한 부분으로 선언해도 이 함수가 저절로 객체에 달라붙는 건 아니며 해당 함수 객체를 참조하는 레퍼런스가 하나 더 생기는 것뿐이다.

### 3.3.3 배열

- 배열은 숫자 인덱싱, 즉 인덱스라는 0 이상의 정수로 표기된 위치에 값을 저장한다.
    - 인덱스는 숫자지만, 배열 자체는 객체여서 배열에 프로퍼티를 추가하는 것도 가능하다.
    - .이나 [] 구문에 상관없이 이름 붙은 프로퍼티를 추가해도 배열 길이에는 변함이 없다.
        - 하지만 배열에 프로퍼티를 추가할 때 프로퍼티명이 숫자와 유사하면 숫자 인덱스로 잘못 해석되어 배열 내용이 달라질 수 있으니 주의하자.
        
        ```jsx
        const myArray = ['foo', 42, 'bar'];
        myArray.baz = 'baz';
        console.log(myArray.length); // 3
        console.log(myArray.baz); // baz
        myArray['2'] = 'hi';
        console.log(myArray); // [ 'foo', 42, 'hi', baz: 'baz' ]
        console.log(myArray[3]); // undefined
        ```
        

### 3.3.4 객체 복사

- 100% JSON-safe 객체는 쉽게 깊은 복사를 할 수 있다.

```jsx
const newObj = JSON.parse(JSON.stringify(someOjb));
```

- 객체의 얕은 복사는 Object.assign()메서드를 사용할 수 있다.

```jsx
const newObje = Object.assign({}, myObject);
```

### 3.3.5 프로퍼티 서술자

```jsx
const myObject = {
  a: 2,
};

// 프로퍼티 서술자 특성 읽기
console.log(Object.getOwnPropertyDescriptor(myObject, 'a'));
// { value: 2, writable: true, enumerable: true, configurable: true }

// 프로퍼티 서술자 특성 직접 수정하여 추가
Object.defineProperty(myObject, 'b', {
  value: 3,
  writable: false, // 쓰기 금지
  configurable: true,
  enumerable: true,
});

console.log(Object.getOwnPropertyDescriptor(myObject, 'b'));
// { value: 3,  writable: false,  enumerable: true,  configurable: true }

myObject.b = 4; // 조용히 실패, 엄격모드였다면 오류 발생

console.log(Object.getOwnPropertyDescriptor(myObject, 'b'));
// { value: 3,  writable: false,  enumerable: true,  configurable: true }

Object.defineProperty(myObject, 'c', {
  value: 5,
  writable: true,
  configurable: false, // 설정 불가
  enumerable: true,
});

delete myObject.c; // 설정 불가하여, 삭제되지 않음

console.log(myObject); // { a: 2, b: 3, c: 5 }

Object.defineProperty(myObject, 'd', {
  value: 6,
  writable: true,
  configurable: true,
  enumerable: false, //해당 프로퍼티 열거 불가, 감추고 싶은 프로퍼티에 한하여 false 설정
});

console.log(myObject.d); // 6

for (const key in myObject) {
  if (Object.hasOwnProperty.call(myObject, key)) {
    console.log(key); // a, b, c
  }
}
```

### 3.3.6 불변성
