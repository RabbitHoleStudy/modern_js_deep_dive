## 객체

JS의 거의 모든것은 객체
객체는 primitive value와 다르게 mutable한 값이며
key: value로 이루어진 property들의 집합

함수도 일급객체이므로 가능하며 메소드라고도 함

프로토타입 기반 객체지향 언어로
- 객체 리터럴
- Object 생성자
- 생성자
- Object.create
- 클래스

등의 방법으로 생성 가능하며 일반적으로
```javascrypt
({...})
```
같은 꼴의 객체 리터럴을 사용   

**식별자 네이밍 규칙을 준수하지 않으면 점 표기법을 사용할수 없기 때문에 규칙 준수를 강력히 권장**

**빈 문자열도 key로 사용할수 있음**

**string이나 simbol이 아닌 값을 key로 사용하면 암묵적으로 string으로 변환되어서 들어감**

**'var' 'function'같은 예약어도 key로 사용 가능하지만 권장하지 않음**

파이썬 TMI
---
내용|파이썬 dictionary|JS object|
|--|---------------|---------|
|key|원시 자료형과 비슷한 imutable value|string, simbol|
|표기법|dict["key"]|obj.key or obj["key"]|
---

메소드
---
다른 언어와 비슷하게 this 키워드를 사용하면 자신을 가리키는 참조변수 사용 가능

프로퍼티
---
존재하지 않는 프로퍼티에 접근하면 undefined 반환   
delete 키워드를 사용해서 삭제 가능

### 축약
``` javascript
let x= 1, y= 2;

// 프로퍼티축약표현 
const obj = { x, y };
console.log(obj); // {x:1, y:2}
```
변수명과 동일한 키를 갖는 오브젝트 생성 가능

### 계산된 프로퍼티

``` javascript
const prefix ='prop';
let i= 0;

// 객체리터럴내부에서계산된프로퍼티이름으로프로퍼티키를동적생성 
const obj = {
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i
};
console.log(obj); // {prop-1: 1,prop-2: 2 ,prop-3: 3}
```