# prototype

## prototype이란? (prototype = 하나의 객체)

상속된 모든 다른 객체들과 공유된 속성을 제공하는 객체

\- 함수의 prototype 프로퍼티가 가리키는 객체를 그 함수의 프로토타입 객체라고 함.
\- prototype 프로퍼티는 기본적으로 빈 객체를 가리킵니다.
\- prototype에 선언된 속성들을 객체는 참조할 뿐임.
\- 객체를 인스턴스화 했을 경우, 인스턴스에서 어떤 속성을 호출하게 되면, 본인에게 없으면 부모객체에 있는지 살펴보고, 부모객체에 없으면 프로토타입에서 찾아 봄.
\- 즉, 인스턴스는 프로토타입의 프로퍼티의 값을 수정할 수 없으며, 자기 자신에 속성을 추가하거나 있는 속성일 경우 자신의 프로퍼티를 참조함.

## 프로토타입 객체의 프로퍼티

함수를 정의하면 함수 객체(생성자)는 prototype 프로퍼티를 갖음.
이 prototype프로퍼티는 프로토타입객체를 가리키며,
이 프로토타입 객체는 constructor와 **proto** 속성을 갖음.
여기서 프로토타입 객체의 constructor는 생성자를 가리키는
순환구조임.

_\*함수로 정의되지 않은 인스턴스는 prototype속성과 constructor 속성이 없음._

## 내부 프로퍼티 [[Prototype]] == **proto**

**proto**값은 그 객체에게 상속을 해 준 부모 객체를 가리킴. 이 연결고리를 프로토타입 체인이라고 함.
여러번의 상속을 거치게 되면, 프로토타입 체인이 발생 하게 되는데 이는 잘못사용하게 되면 단점이 될 수 있음.

## prototype을 사용하는 이유

여러객체에서 공유할 수 있는 함수/변수가 있을 경우 사용하면 같은 메모리를 공유하므로 메모리 자원을 절약

- prototype의 단점
  prototype chain으로 발생되는 연쇄적인 검색은 자원소모가 생김.
  기본적인 값은 prototype에 명시하고 자주사용되는 속성들은 자신에게 명시하여 사용하는 것이 좋음.

## prototype 상속방법

- 생성자로 객체를 생성할 때 생성자의 prototype프로퍼티에 추가하는 방법
- Object.create메서드로 상속을 받을 프로토타입을 지정하는 방법

## prototype 관련 속성

- instanceof (객체 instanceof 생성자)
- isPrototypeOf (프로토타입객체.isPrototypeOf(객체))
  특정 객체가 그 객체의 프로토타입 체인에 포함되어 있는지 여부를 boolean으로 반환.
  즉, new, apply, call로 생성된 것인지 판단.

```javascript
function F() {}
var obj = new F();

console.log(obj instanceof F); //true
console.log(obj instanceof Object); //true
console.log(obj instanceof Date); //false

console.log(F.prototype.isPrototype(obj)); //true
console.log(Object.prototype.isPrototype(obj)); //true
console.log(Date.prototype.isPrototype(obj)); //false
```

## 객체의 프로토타입을 반환(ES5).

```javascript
Object.getPrototypeOf(friend);
```

## 프로토타입 설정(ES6)

인스턴스화 이후 프로토타입이 변경하지 않을 것이라는 가정에서 변경가능으로 바뀜.
Object.setPrototypeOf();

```javascript
var person = {};
var dog = {};
let friend = Object.create(person);
Object.setPrototypeOf(friend, dog);
console.log(Object.getPrototypeOf(friend)); // dog
```
