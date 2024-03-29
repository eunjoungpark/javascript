# function

## 함수선언 방식의 차이

함수리터럴로 선언 되었을때, 함수의 끌어올림(hoisting)이 발생하지 않음.

```javascript
    //1. 일반함수 선언
    function test(){
        do something ...
    }

    //2. 함수 리터럴
    var test = function(){
        do something ...
    }
```

## Function 생성자

Function 생성자는 전역변수와 자신의 지역변수만 읽고 쓸 수 있다는 단점이 있으며 악의적으로 악성코드가 실행될 수 있는 보안문제가 있음.

```javascript
var fn = new Function("a", "b", "return a+b");
```

## 함수객체 프로퍼티

- caller : 현재 실행 중인 함수를 호출한 함수
- length : 함수의 인자 개수
- name : 함수를 표시할 때 사용하는 이름
- prototype : 프로토타입 객체의 참조

## 중첩함수

함수를 이중이상 겹쳐 선언한 것으로 전역에 선언된 함수를 외부함수, 그 안에 선언된 함수를 중첩함수(내부함수)라 함.
내부함수는 **외부함수의 선언된 변수 및 함수를 참조할 수 있고** 내부함수의 변수를 은닉할 수 있음.

## arguments

함수의 인수 arguments는 callee와 length라는 프로퍼트를 갖는데, callee는 arguments가 속한 함수를 가리킴.

callee는 익명함수를 재귀적으로 호출할 경우 유용함.

## 전역환경과 전역객체

var로 선언된 변수와 함수는 **전역환경**에 정의되어 delete로 삭제할 수 없음.
하지만, var로 선언되지 않은 변수는 전역객체에 선언되어 delete가 가능.

## 실행문맥

중첩함수의 경우 외부 함수와 내부 함수 각각 서로 다른 실행문맥에 선언됨.

## 클로저

### 클로저가 되기 위한 조건

1. 외부함수와 내부함수로 정의된 상태에서
2. 내부함수가 외부함수의 변수를 참조, 이 내부함수를 반환하게 함.
3. 이 내부함수를 전역변수가 참조하면서 가비지컬렉터가 일어나지 않게 되고,
4. 데이터가 삭제되지 않고 유지됨.
   _\*내부함수 객체가 외부함수의 프로퍼티를 참조하고 전역변수가 간접적으로 객체를 참조하면서 가비지 컬렉터가 되지 않음._

## 가비지컬렉터

객체를 생성하면 메모리 공간이 동적으로 확보됨. 사용하지 않는 객체의 메모리 영역은 가비지 컬렉터가 자동으로 해제함.

## apply vs call vs bind

this와 인수를 이용해서 함수를 실행.

```javascript
function TestFunc(arg1, arg2) {
  console.log(arg1 + arg2 + this.name);
}

var person = {
  name: "park"
};

var person2 = {
  name: "eun"
};

//call과 같이 인수를 전달할 수 있으나, 객체로 바인딩만 하고 바로 실행하진 않음.
var result = TestFunc.bind(person, "hello ", "just bind ");
result(); //나중에 필요할 때 실행.

// ()를 이용해 바로 실행할 수도 있음.
TestFunc.bind(person2, "Hello ", "eunjoung ")();

//,로 구분되는 문자열형태, 함수 바로 실행
TestFunc.call(person, "hello ", "eunjoung ");

//배열형태 인수를 전달, 함수 바로 실행
TestFunc.apply(person, ["hello ", "eunjoung2 "]);
```
