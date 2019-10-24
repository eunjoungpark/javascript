#Array

##배열을 생성하는 방법
생성자로 생성할 때, 인수가 한개고 정수이면 배열의 길이를 의미함.
```javascript
var array = [1,2,3];
var arr = new Array(3);
```

##배열을 액세스 하는 방법
for문 for-in문으로 가능.
```javascript
array.forEach(function(element){
    console.log(element);
});

```

##push, pop, shift, unshift
###push : 
배열 마지막에 새로운 요소를 추가
```javascript
array.push(4);
console.log(array, "\n");
```

###pop : 
배열의 마지막 요소를 추출(반환), 배열에 영향을 줌
```javascript
console.log(array.pop());
console.log(array, "\n");
```

###shift : 
배열 첫번째 요소를 추출(반환), 배열에 영향을 줌
```javascript
console.log(array.shift());
console.log(array, "\n");
```

###unshift : 
배열 첫번째에 새요소를 추가
```javascript
console.log(array.unshift(0));
console.log(array, "\n");
```

###indexOf : 
배열에서 색인하여 위치를 반환
```javascript
console.log(array.indexOf(3)); //3은 2에 위치하여 2반환.
```

###splice(start, count) : 
원하는 위치의 값을 반환(배열타입). count를 설정하지 않으면 시작에서 끝까지 반환, 배열에 영향을 줌
```javascript
var array2 = [0,1,2,3,4];
console.log(array2.splice(2));
console.log(array2);
```

###slice(start, end) : 
원하는 위치의 값을 반환, 배열에 영향을 주지 않음.
```javascript
var array3 = [0,1,2,3,4];
console.log(array3.slice(2,4)); //[2, 3]
console.log(array3);
```

###filter() : 
어떤 조건에 부합한 요소들만 추출하여 새배열로 반환, 배열에 영향을 주지 않음.
```javascript
var array4 = [0,1,2,3,4];
console.log(array4.filter(function(item){
    return item > 2; //조건문과 반환문이 있음.
}));
console.log(array4);
```

###map() : 
모든 배열요소에 어떤 처리를 하여 새배열을 반환, 배열에 영향을 주지 않음.
```javascript
console.log(array4.map(function(item){
    return item * 2; //처리문과 반환이 있음.
}));
console.log(array4);
```

###reverse() : 
배열을 역순으로 변경. 원본배열에 영향을 줌.
```javascript
console.log(array4.reverse());
console.log(array4);
```

###concat() : 
두 배열을 단일배열로 만들어 새로운 배열로 반환. 원본배열에 영향이 없음.
```javascript
var newArray = ["join", "me"];
var oldArray = [1,2,3,4,5];

console.log(newArray.concat(oldArray)); //["join", "me", 1, 2, 3, 4, 5]
```

###join() : 
배열을 문자열로 변환, 배열사이에 주어진 값를 삽입. 원본배열에 영향이 없음.
```javascript
console.log("join \n");
console.log(newArray.join(oldArray)); //join1,2,3,4,5me
```

###reduce(total, value) : 
수식을 이용해 배열을 하나의 값으로 축소, 원본배열에 영향 없음.
```javascript
console.log(oldArray.reduce(function(tot, val){ // 15반환
    return tot + val;
}));

console.log(oldArray.reduce(function(tot, val){ // 25반환
    return tot + val;
}, 10)); //초기값을 설정하면 첫번째 더할 숫자가 설정됨.
```

###희소배열 : 순차적으로 생성되지 않은 배열을 희소배열이라고 함.
``` javascript
var a = [1,2,3];
a[4] = 4;
console.log(a.length); //5 (배열의 갯수인 4가 아니라 5가 출력)
```

###배열도 객체
* 배열도 객체이기에 fon-in과 hasOwnProperty, delete, push, 속성추가등이 가능.
* 배열과 객체의 차이점은 배열은 length속성이 있으며,
    __proto__가 각각 Array, Object로 다름.

```javascript
var a = [1,2,3];
// a[4] = 4;
console.log(a);

var b = {
    0 : 1,
    1 : 2,
    2 : 3
}
console.log(b);
```
