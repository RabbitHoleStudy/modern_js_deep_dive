## 타입 변환

JS의 모든 값은 타입을 가진다.

### 명시적 타입 변환(Explicit Coercion, Type Casting)

**coercion : 강제**

```jsx
var x = 10;
var str = x.toString();
```

### 암묵적 타입 변환(Implicit Coercion, Type Coercion)

```jsx
var x = 10;
var str = x + ""; // string
```

JS 엔진이 알아서 평가한다. 재할당이 아닌, 새로운 주소에 형변환된 타입을 갖는 값을 할당한다는 점을 인지하자.

### 코드 문맥에 따른 형변환

```jsx
'10' + 2 // '102'
2 + '10' // '210'
5 * '10' // 50
'10' * 5 // 50
!0 // true
```

### Truthy, Falsy

참으로 평가되는 값, 거짓으로 평가되는 값을 말한다.

```jsx
'' // Falsy
true // Truthy
0 // Falsy
'sadfasdf' // Truthy
null // Falsy
```

## 단축 평가

```jsx
'Cat' && 'Dog' // "Dog"
```

논리곱(&&), 논리합(||)은 모두 좌항→우항으로 평가한다.

평가 특성(AND, OR)에 따라 ‘결과를 정하는 항’값을 반환한다.

논리 연산의 결과를 결정하는 피연산자(결과가 되는 항)를 타입 변환하지 않고 그대로 반환한다. 이를 단축 평가라고 한다.

```jsx
var done = true;
var message = '';

if (done) message = '완료'; // 일반적인 생각

message = done && '완료'; // 단축 평가의 반환 값을 이용한 방법 
```

### 언제 쓸까? - 프로퍼티를 참조하는 객체의 null 여부를 이용

```jsx
var elem = null;
var value = elem && elem.value; // null
```

개인적인 생각으로는 이런 방식으로 표현하는 것보다, 명확하게 삼항 연산자를 사용하여 false인 경우에 값이 어떻게 되는지를 표현하는게 더 좋을 것 같다.

## 옵셔널 체이닝 - `?.`

옵셔널 체이닝 연산자인 `?.`은 피연산자인 좌항이 `null || undefined`인 경우에 `undefined`를 반환하고, 그렇지 않으면 `우항의 프로퍼티 참조`를 반환하는 연산자다.

근데 `undefined`가 나온다는 얘기는 어딘가에 값을 할당해서 보여준다는 얘기인데, `elem?.value`에서 `value`는 사실상 지정되지 않은 값이란 말이지. 그렇다면 이 `undefined`는 도대체 어디에서 나오는 걸까?

→ `undefined` 값의 경우에도 JS 엔진에서 `undefined`를 메모리에 할당해서 나타내는 거잖아. `elem?.value`를 사용할 때에 이 `undefined` 값은 어떻게 할당되는걸까?

<img width="739" alt="1" src="https://github.com/RabbitHoleStudy/modern_js_deep_dive/assets/105692206/294ccc9d-93bd-42b2-9a98-b171f65851ff">


그러면 JS 엔진 자체에서도 코드 평가를 시작할 때에 C의 `void*(0)`과 같은 `null` 값을 미리 가지고 있는 것 처럼 `undefined`라는 값을 가지고 있는 메모리 주소가 static하게 지정되어 있는거야?

<img width="720" alt="2" src="https://github.com/RabbitHoleStudy/modern_js_deep_dive/assets/105692206/5b40cfe1-c690-4a76-8e8e-0eec53461767">


그러면 `elem?.value`가 나타내는 `undefined`값은 어떤 메모리 주소를 가리키고 있는거야?

<img width="721" alt="3" src="https://github.com/RabbitHoleStudy/modern_js_deep_dive/assets/105692206/7f3da590-fd0a-482e-8d7d-3d2319df3964">


---

```jsx
var elem = null;
elem?.value ? elem.value : null
```

결국 `undefined`라는 값으로 평가해버리니까, 값을 통제한다는 명시적인 뉘앙스를 코드에 적용하기 위해서는 별도의 `null`처리를 위와 같이 해볼 수 있을 것 같다.

→ 그런데 value라는 프로퍼티는 애초에 없는데 `undefined`로 두는게 나을 것 같기도 하고.

```jsx
var str = '';
var length = str && str.length; // ret: str === ''
console.log(length); // ''

var length = str?.length; // str != null && != undefined, 프로퍼티 참조 진행
console.log(length) // 0
```

## 널 병합 연산자 `??`

연산자 `??`는 좌항의 피연산자가 `null || undefined`인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 그대로 반환한다.

```jsx
var foo = null ?? 'default string';
console.log(foo); // "default string"

var hello = "hello";
var bar = hello ?? "hello is null or undefined";
console.log(bar); // "hello"
```
