## 타입

JS의 모든 값은 타입을 갖는다.


JS는 number라는 하나의 숫자 타입만 존재한다.

→ **모든 수를 실수로 처리**한다 - 정수로 표시되어도 그것은 실수다 - 정수로 표시되는 수 끼리 나누어도 실수가 나올 수 있다.

타입을 가져야하는 이유는,

- 값을 **`저장할 메모리 공간의 크기`**를 결정하기 위해
- 참조할 때 `읽어올 메모리 공간의 크기`를 결정하기 위해
- 메모리에 담긴 `2진수를 어떻게 해석할지` 결정(타입에 따른 해석)하기 위해

필요하다.

## 템플릿 리터럴

백틱(````)을 이용한 문자열 표현을 말한다.

일반 문자열과는 다르게 이스케이프 시퀀스를 사용하지 않더라도 그대로 표현하듯이 사용할 수 있다.

## 동적 타이핑

JS의 **변수는 선언이 아닌 할당에 의해 타입이 결정**(추론, inference) 된다.

또한 해당 **변수는 재할당을 통해 언제든지 동적으로 변할 수 있다**.

즉 변수는 타입을 가지지는 않지만, 해당 값이 타입을 가지는 것이다. 

동적 타입 언어에서 변수는 타입을 갖는 값에 대한 별명일 뿐이다.
