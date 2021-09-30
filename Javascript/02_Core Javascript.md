#Core Javascript(정재남 님 강의)
## 1. 데이터 타입
- 자바스크립트 메모리구조
  - Stack Memory
    - 변수, 기본형 데이터, 정적할당   
  - Heap Memory
    - 참조형 데이터, 동적할당


- 자바스크립트 데이터타입
  - Primitive Type(기본형)
    - Number
    - String
    - Boolean
    - null
    - undefined
    - Symbol
  - Reference Type(참조형)
    - Object
      - Array
      - Function
      - RegExp
      - Set/WeakSet
      - Map/WeakMap
      - ... 

![image](https://user-images.githubusercontent.com/59413128/135451716-e68b0078-bf48-45b9-aa97-6e26c7be2c26.png)
기본형에 비해서 참조형이 메모리 할당 과정에 1단계를 더 거치기 때문에, 기본형은 값이 바로 변하지만 참조형은 값이 변하지 않는다.

![image](https://user-images.githubusercontent.com/59413128/135453678-e4bf9b79-bd93-43e3-9fcf-2a11920780b8.png)
obj.arr='str'으로 재할당하면,
5004는 참조카운트가 0인 메모리가 된다. 이런 메모리는 Garbage Collecting의 수집대상이 되어 언젠가 자연스럽게 사라진다.
또한, 5004가 사라지면서 '8104~?'도 참조카운트가 0이 되며 Garbage Collecting의 수집대상이 되어 사라진다.

![image](https://user-images.githubusercontent.com/59413128/135453974-ef4ab2bf-f923-4b57-922e-0f24b13c46c8.png)
똑같은 값의 주소를 참조한다.

값을 직접 저장할 때는 데이터 할당시에는 빠르나, 비교에 비용이 많이 들고, 메모리 낭비가 심하다는 단점이 있다.
그래서 실제로는 값을 직접 저장하지 않고 값의 주소를 저장하여 데이터 할당시에는 느리나, 비교에 비용이 들지 않고, 메모리 낭비를 최소하는 장점을 취한다.
따라서 같은 값이 전체 메모리 공간상에 오직 하나만 존재한다. 이것이 곧 불변값을 의미한다.
그래서 기본형 데이터가 불변값이라고 하는 것이다.

이러한 이유로 객체를 복사하고 복사한 객체 값을 바꿨는데 원본 객체의 값이 같이 바뀐다.
이를 어떻게 해결할까라는 고민 지점에서 매번 새로운 객체를 만드는 '불변객체' 가 나타났다. 

![image](https://user-images.githubusercontent.com/59413128/135455980-6256890b-f3eb-4192-a64d-d9c1989af1d1.png)

## 2. 실행 컨텍스트 (execution context)
실행 컨텍스트는   코드를 실행하는 데에 필요한 배경이 되는 조건/환경이다.

stack은 아래처럼 제일 마지막에 들어온 게 제일 먼저 빠지고, 제일 먼저 들어온 게 제일 마지막에 빠지는 개념이다.
코드 실행에 관여하는 스택인 call stack은 현재 어떤 함수가 동작중인지, 다음에 어떤 함수가 호출될 예정인지 등을 제어하는 자료구조이다.
![image](https://user-images.githubusercontent.com/59413128/135457526-892230f5-73d0-4188-adb1-0f0555523fe1.png)

실행 컨텍스트에는 세 가지 환경정보들이 담긴다.
- VariableEnvironment : 식별자 정보 수집(값의 변화 실시간 반영X)
- LexicalEnvrionment : 각 식별자의 '데이터' 추적(값의 변화 실시간 반영O)
- ThisBinding
