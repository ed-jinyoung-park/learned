## var, let, const

1. var는 함수 레벨 스코프인 반면, let과 const는 블록 레벨 스코프이다.
2. var는 호이스팅이 되는 반면, let과 const는 호이스팅되지 않는다.
3. var는 동일한 이름으로 변수를 선언해도 에러가 나지 않는 반면, let과 const는 동일한 이름으로 변수를 선언하면 에러가 난다.(let으로 선언한 변수를 const로 다시 선언한 경우 에러)
4. const는 반드시 초기값을 할당해주어야 하며, 변경이 불가능하다.



### 호이스팅

변수와 함수의 **선언** 부분을 위로 끌어올리는 것. (``var``로 선언한 경우에 해당)

다음과 같은 코드를 실행할 경우

```javascript
console.log(a());
console.log(b());

function a(){
    return 'a';
}

var b = function bb(){
    return 'bb';
}
```

아래와 같이 호이스팅 된다. 변수 b,c는 호이스팅되어 ``console.log()`` 부분에서 ``undefined`` 로 찍히게 된다.

```js
function a(){
    return 'a';
}

var b;

console.log(a()); // 'a'
console.log(b()); // undefined

b = function bb(){
    return 'bb';
}

```

* 함수 선언문의 경우 통째로 호이스팅된다.
* 함수 표현식의 경우 변수만 호이스팅되고 함수 할당은 코드 순서대로 이루어진다.

* ``let, const``의 경우 실제로는 호이스팅이 일어나지만 값이 할당되기 전까지 TDZ(temporal dead zone: 임시 사각지대)에 있기 때문에 일어나지 않는 것처럼 처리된다. 따라서 선언 전에 변수를 사용하려고 하면 에러가 난다.