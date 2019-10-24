#DOM
##요소가져오기
* firstElementChild
* lastElementChild
* nextElementSibling
* parentElement
* getElementsByTagName('li')
* getElementsByClassName('simple')
* getElementById('simple')
* querySelector('h1')
* querySelectorAll('h1')

##요소생성하기
* createElement
* element.textContent
* target.appendChild(element)
* target.insertBefore(element)
* target.insertAfter(element)

##요소삭제하기
* target.remove();
* parentElement.removeChild(element);

##이벤트
이벤트 핸들러와 이벤트 리스너는 다름.
이벤트 리스너는 이벤트에 함수를 연결하거나 제거 할 수 있음.
```javascript
function test(){
    console.log("test");
}
element.click = test; //이벤트 핸들러 방식
element.addEventListener('click',test); //이벤트 리스너 방식
element.removeEventListener('click',test);
```