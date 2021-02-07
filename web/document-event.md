## 문서와 리소스 로딩 이벤트

> DOMContentLoaded, load, beforeunload/unload



### DOMContentLoaded

* DOM 트리가 완성되었을 때 발생한다.

* HTML 문서에 있는 script를 모두 완료한 다음에 발생한다.

* 외부 CSS가 로드되는 것은 기다리지 않는다.

  * 단, 스타일시트 태그 바로 뒤에 있는 스크립트는 스타일시트가 로딩될때까지 기다린다.

    ```html
    <link type="text/css" rel="stylesheet" href="style.css">
    <script>
      // 이 스크립트는 위 스타일시트가 로드될 때까지 실행되지 않습니다.
      alert(getComputedStyle(document.body).marginTop);
    </script>
    ```

    

**DOMContentLoaded를 막지 않는 스크립트**

* async 속성이 있는 스크립트는 DOMContentLoaded를 막지 않는다.
* ``document.createElement('script')`` 로 동적으로 생성된 스크립트는 DOMContentLoaded를 막지 않는다.

동적으로 DOM을 생성하고 ``appendChild``하는 코드가 있는 경우에도 ``appendChild``가 다 실행된 다음에 ``DOMContentLoaded`` 이벤트가 발생한다.

```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <div id="app">App</div>
  <script>
    document.addEventListener("DOMContentLoaded", () => {
      alert(document.querySelectorAll('.new').length); // 10000
    });
  </script>
  <script>
      for(let i=0; i<10000; i++){
      const newEl = document.createElement('div');
      newEl.className = 'new';
      newEl.innerHTML = `wow`;
      document.querySelector('#app').appendChild(newEl);
    
      }
  </script>
</body>
</html>
```



### load

* 이미지, css 등의 리소소가 완전히 로딩된 다음 발생한다.
* ``window.onload = function(){}`` 혹은 ``window.addEventListener('load',(e) => {})``로 확인할 수 있다.



### beforeunload

* 현재 페이지를 떠나 다른 페이지로 이동할 때나 창을 닫으려고 할 때 발생한다.
* 페이지를 떠나기 전 사용자에게 확인을 요청할 때 쓰인다.



### unload

* 사용자가 문서를 완전히 닫을 때 실행된다.
* 이 시점에 ``navigator.sendBeacon(url, data)`` 를 활용해 분석정보를 서버로 보낼 수 있다.



### readyState

로딩 상태를 알려주는 document의 프로퍼티.

* ``"loading"`` : 문서를 불러오는 중
* ``"interactive"`` : 문서가 완전히 불러짐. DOMContentLoaded 이벤트가 실행되기 바로 직전에 변경됨.
* ``"complete"`` : 문서를 비롯한 이미지 등의 리소스도 모두 불러짐. load 이벤트가 실행되기 바로 직전에 변경됨.


### Reference
* https://ko.javascript.info/onload-ondomcontentloaded