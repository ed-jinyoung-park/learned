## 클로저
> 함수가 자신의 렉시컬 스코프를 기억하여 렉시컬 스코프 밖에서 호출해도 접근할 수 있는 기법

```js
function outer(c) {
  let a = 1;

  function inner() {
    let b = 2;
    return a + b + c;
  }
  return inner();
}

console.log(outer(3)); // 6

```

outer 함수를 실행하면 inner함수의 호출값이 리턴되는 구조이다.

inner 함수에서는 변수 a,b,c를 사용하는데 b는 inner 함수 내부에 할당되어 있지만,

a와 c가 할당되어 있지 않다. 변수 a,c가 없으면 스코프체인을 통해 상위스코프인 outer 함수 내부에서 찾게된다. 이렇게 전역스코프까지 찾게 된 다음 없으면 undefined를 리턴한다.

이런식으로 inner함수는 생성한 시점의 스코프(outer)를 기억해서 사용할 수 있다.

클로저는 상태유지, 전역 변수의 사용 억제, private한 변수 활용에 사용된다.

```html
<!DOCTYPE html>
<html>

<body>
  <p>전역 변수를 사용한 Counting</p>
  <button id="inclease">+</button>
  <p id="count">0</p>
  <script>
    var incleaseBtn = document.getElementById('inclease');
    var count = document.getElementById('count');

    // 카운트 상태를 유지하기 위한 전역 변수
    var counter = 0;

    function increase() {
      return ++counter;
    }

    incleaseBtn.onclick = function () {
      count.innerHTML = increase();
    };
  </script>
</body>

</html>
````

다음과 같은 경우에 함수가 호출될때마다 counter 값이 증가되어 그 값을 유지할 수 있다.

만약 couter가 increase()안에 선언되어 있을 경우 버튼을 계속 눌러도 counter는 1에서 멈춘다. 매번 새로 0으로 선언,할당되는 꼴이다.