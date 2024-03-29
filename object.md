# Object

## 객체가 생성되는 과정

1. obj를 새로 생성 된 네이티브 ECMAScript 객체로 둡니다.
2. 8.12에 명시된대로 obj의 모든 내부 메소드를 설정하십시오.
3. obj의 [[Class]] 내부 속성을 "Object"로 설정합니다.
4. obj의 [Extensible]] 내부 속성을 true로 설정합니다.
5. prototype은 "prototype"인수로 F의 [[Get]] 내부 속성을 호출하는 값이됩니다.
6. Type (proto)이 Object이면 obj의 [Prototype] 내부 속성을 proto로 설정합니다.
7. Type (proto)이 Object가 아닌 경우 15.2.4에서 설명한대로 obj의 [[Prototype]] 내부 속성을 표준 내장 객체 프로토 타입 객체로 설정합니다.
8. result가 F의 [[Call]] 내부 속성을 호출 한 결과가되게하고 obj를이 값으로 제공하고 [[Construct]]로 전달 된 인수 목록을 args로 제공합니다.
9. Type (결과)이 Object이면 결과를 반환합니다.
10. obj를 반환합니다.

## 객체를 생성하는 방법

```javascript
//1. 객체리터럴 방식
var obj = {};

//2. 생성자 방식
var obj = new Object();

//3. Object.create(null)
var obj = Object.create(null); //프로퍼티 & 프로토타입이 정의되지 않은 빈객체 생성.
var obj = Object.create(Object.prototype); //Object.prototype이 있는 빈 객체 생성.
function Person() {
  this.name = "eunjoung";
}
var person = Object.create(Person.prototype); //사용자 정의 객체 할당
```

## 객체 속성 및 접근법

객체 내에 속성유형은 모두선언 가능

```javascript
var card = {
  suit: "something",
  hobbies: ["cycle", "sing"],
  status: function() {
    return "good";
  },
  "nick-name": "zzangsuni"
};

//1. card.suit   .연산자
//2. card["suit"]   []연산자
//3. card.status();
//4. card["nick-name"]);  문자열("")로 된 키워드를 사용할 때 유용
```

## 선언되지 않은 변수 또는 프로퍼티 참조

```javascript
//1. 객체속성 참조의 경우
var obj = {};
console.log(obj.a); //undeined

//2. 변수 참조의 경우
console.log(a); //Uncaught ReferenceError: testSomething is not defined
```

## 생성자란

new키워드로 객체를 생성할 것을 기대하고 만든 함수를 의미.
생성자로 만든 객체를 인스턴스라고 하며 이것을 객체지향언어에서 실체라 표현함.

```javascript
var obj = new Object(); //obj는 인스턴스이며 실체임.
```

## 생성자 메소드정의 문제

정의된 메소드가 모든 인스턴스마다 메소드가 생성되므로 메모리낭비가 됨.

## 생성자 메소드정의 해결책

prototype : 함수객체에 있는 속성으로, 상속된 모든 다른 객체들과 공유된 속성을 제공하는 객체

## 객체관련 속성

- hasOwnProperty 속성
  객체를 for-in으로 순환하면 prototype(부모 객체에서 상속된)에 명시된 속성들도 순환함.
  hasOwnProperty 속성을 이용하면, 해당 객체에 속한 속성인지 boolean으로 반환.
  (상속받은 속성이면 false반환)

```javascript
Object.prototype.job = "programer";
var obj = {
  name: "eun",
  age: 30
};
for (pro in obj) {
  console.log(pro); // name, age, job
  console.log(obj1.hasOwnProperty(pro)); // true true false
}
```

- Object.keys(obj)
  지정한 객체에 열거가능한 속성만 배열로 반환.

```javascript
var obj = {
  name: "eun",
  age: 30,
  sayHello: function() {}
};
Object.defineProperty(obj, "sayHello", { enumerable: false });
console.log(Object.keys(obj)); // ["name","age"]
```

- Object.getOwnPropertyNames
  지정한 객체의 프로퍼티 중에 열거가능 여부와 상관없이 배열로 반환

```javascript
console.log(Object.getOwnPropertyNames(obj));
//["name","age","sayHello"]
```

- in 연산자
  in은 자신의 프로퍼티외에 Object 내에 속성까지 존재여부를 true or false로 반환.
  in 연사자는 객체의 프로토타입이 null프로토타입을 가지는 객체에 사용하는 경우에만 안전.

```javascript
Object.prototype.job = "programer";
var obj = {
  name: "eun",
  age: 30
};
console.log("name" in obj); //true
console.log("age" in obj); //true
console.log("job" in obj); //true
console.log("toString" in obj); //true
```

## Object.create(null)

생성자(new)방식으로된 함수 객체를 상속받지 않고, 객체러터럴방식의 객체를 상속받음.

```javascript
var anotherPerson = {
  name: "park",
  age: 37,
  myname: function() {
    console.log("My name is" + this.name);
  }
};

function anotherPerson2() {
  this.name = "park";
  this.age = 37;
}

var person = Object.create(); //괄호안에 아무것도 정의히자 않으면, 오류
var person = Object.create(null); //null로 선언시, 아무것도 없는 빈객체 생성.
var person1 = Object.create(anotherPerson); //anotherPerson의 속성들을 상속, 함수형이 아니여서 프로토타입은 상속은 없음.
var person2 = Object.create(anotherPerson2.prototype); //anotherPerson2의 프로토타입만 상속, anotherPerson2 멤버프로퍼티 사용X
```

## Object.defineProperty()

특정 객체의 속성을 세부적으로 설정할 수 있는 속성

```javascript
var account = {
    cash : 12000,
    _name : 'Default',
    withdraw : function(amount){
        this.cash -= amount;
        console.log('withdrew ' + amount + ', new cash reserve is: '+ this.cash) ;
    }
}

Object.defineProperty(account, 'name', {
    value : something, [값설정]
    writable : true of false, [값변경 가능여부]
    enumerable : true of false, [순회가능여부]
    configurable : true of false, [재정의 및 삭제가능여부]
    get:function(){
        return 'hello';
    },
    set:function(name){
        if(name == 'Max'){
            this._name = name;
        }
    }
});

console.log(account.name); //hello
console.log(account._name); //Default
```

## Object.defineProperties()

여러개의 프로퍼티를 한꺼번에 설정

```javascript
var person = Object.defineProperties(
  {},
  {
    _name: {
      value: "Tom",
      writable: true,
      enumerable: true,
      configurable: true
    },
    name: {
      get: function() {
        return this._name;
      },
      set: function(value) {
        var str = value.charAt(0).toUpperCase() + value.substring(1);
      },
      enumerable: true,
      configurable: true
    }
  }
);
Object.getOwnPropertyDescriptor(person, "name");
```

## Object.getOwnPropertyDescriptor(객체, 프로퍼티 이름);

그 객체의 프로퍼티 디스크립터만 가져옴(부모속성 X)

```javascript
Object.getOwnPropertyDescriptor(person, "name");
//{enumberable : true, configruable : true}
```

## 객체 종류

### 네이티브 객체 : ECMAScript 사양에 정의된 객체

- Object
- String
- Number
- Boolean
- Array
- Function

### 호스트객체 : ECMAScript에 정의되어 있지 않지만 자바스크립트 실행 환경에 정의된 객체

- Window
- Navigator
- History
- Location
- DOM에 정의된 객체
- Ajax를 위한 XMLHttpRequest객체
- HTML5의 API
