# 2장. 의미 있는 이름

- 한 개념에 한 단어를 사용하라.

# 3장. 함수

- 함수를 작게 만들어라.
    - 함수에서 들여쓰기 수준은 1단이나 2단을 넘어서면 안 된다. 그래야 함수는 읽고 이해하기 쉬워진다.
- 함수는 한 가지만을 해야 한다.
    - 함수가 한 가지만 하는지 판단하는 방법이 있다. 단순히 다른 표현이 아니라 의미 있는 이름으로 다른 함수르 추출할 수 있다면 그 함수는 여러 작업을 하는 셈이다.
- 함수 당 추상화 수준은 하나로
    - 함수가 확실히 한 가지 작업만 하려면 함수 내 모든 문장의 추상화 수준이 동일해야 한다.
    - 한 함수 내에서 추상화 수준을 섞으면 특정 표현이 근본 개념인지 아니면 세부사항인지 구분하기 어려워 헷갈리기 때문이다.
- 위에서 아래로 코드 읽기: 내려가기 규칙
    - 코드는 위에서 아래로 이야기처럼 읽혀야 좋다. 한 함수 다음에는 추상화 수준이 한 단계 낮은 함수가 온다.
- 서술적인 이름을 사용하라!
    - 이름이 길어도 괜찮다. 길고 서술적인 이름이 짧고 어려운 이름보다 좋다.
    - 이름을 붙일 때는 일관성이 있어야 한다. 모듈 내에서 함수 이름은 같은 문구, 명사, 동사를 사용한다.
- 함수 인수
