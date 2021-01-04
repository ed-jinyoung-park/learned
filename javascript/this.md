# this

자바스크립트의 함수는 호출될 때, 매개변수로 전달되는 인자 값 이외에 ``arguments``객체와 ``this``를 암묵적으로 받는다.

여기서 ``this``는 특정 객체를 가리키는데 어떤 객체를 가리키는지는 함수 호출 방식에 의해 동적으로 결정된다.

동적으로 결정되는 방식은 크게 4가지가 있다.

이를 정리하자면 

1. 기본적으로 ``this``는 전역 객체를 가리킨다.
2. 객체의 메소드에서 사용하면 해당 객체를 가리키게 된다.
3. 생성자를 통해 만든 인스턴스에서 사용하면 해당 인스턴스를 가리키게 된다. 
4. ``apply``,``bind``,``call``의 메소드로 ``this`` 가 가리키는 객체를 바인딩할 수 있다.



 ```javascript
function foo(){
    console.log(this);
}

// 1. 함수 호출
foo(); // global

var obj = {
    foo: function(){
        // 2. 메소드 호출
        console.log(this) // obj
        
        // 메소드가 아닌 메소드의 내부함수 호출 
        function bar(){
            console.log(this) // global
        }
    }
}

// 3. 생성자 호출
var instance = new foo(); // foo



 ```



#### apply, call , bind

this를 바인딩할 수있는 메소드이다.

``apply``와 ``call``의 차이점은 arguments를 배열로 받느냐, 인자들로 받느냐이다.

```javascript
func.apply(thisArg, [argsArray])

// thisArg : 함수 내부의 this에 바인딩할 객체
// argsArray : 함수에 전달할 argument의 배열
```

```js
func.call(thisArg[, arg1[,arg2[,...]]])

// thisArg : 함수 내부의 this에 바인딩할 객체
// arg1 , arg2 : 함수에 전달할 argument들
```

```js
function Person(name, job){
    this.name = name;
    this.job = job;
}

var jinyoung = {};
Person.apply(jinyoung, ['진영','developer']);
Person.call(jinyoung, '진영','developer');

// jinyoung.name : '진영'
// jinyoung.job : 'developer'
```

``bind``는 es5에서 나온 문법으로 this가 바인딩된 새로운 함수를 리턴해준다.

```js
func.bind(thisArg[, arg1[, arg2[, ...]]])
```

```js
var jy = {};
Person.bind(jy)('진영','developer');
```



#### arrouw function

arrow function에서는 ``함수이름``, ``this``와 ``arguments``가 없다. 

arrow function에서 ``this``를 쓰게 되면 ``this``가 없으므로 스코프 체인을 순서대로 뒤져가면서 상위 스코프로 올라가 ``this``가 있는지 찾게 된다.

따라서 arrow function에서의 ``this``는 상위 스코프의 ``this``를 대신 가리키게 된다.

```js
const btn = document.querySelector('#btn');

const obj = {
    count: 0
	btn.addEventListener('click',()=> {
    	console.log(this); // obj
	})
    
    btn.addEventListner('click',function(){
        console.log(this); // btn
    })
}
```

