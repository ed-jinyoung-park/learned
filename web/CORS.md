## CORS(Cross Origin Resource Sharing)

> 교차 출처 자원 공유 . 보안 취약점을 공격할 수 있는 방법(CSRF, XSS)을 막기 위해 생겨난 정책

### Same Origin Policy

URL은 Protocol+Host+Port+Path+QueryString+Fragment로 이루어져있는데, 

이때 **Protocol과 Host, Port**가 같으면 Same origin이다.

통신간에 공격을 방지하기 위해 같은 출처인 경우에만 리소스를 받을 수 있게 하는 정책이다.

SOP 확인은 브라우저에서 일어나며, request header의 ``origin``과  response header의 ``Access-Control-Allow-Origin``이 같으면 같은 출처로 인식한다.



**예외 조항(SOP를 지키지 않아도 받을 수 있는 요청과 리소스)**

* CORS 정책을 지킨 요청
* 실행 가능한 스크립트
* 렌더될 이미지
* 스타일 시트



**SOP 예시**

https://jinyoung.kr라는 URL이 있을 때,

* https://jinyoung.kr/bookmark (O)

* http://jinyoung.kr (X - protocol이 다르다.)

* https://jinyoung.kr:4433/bookmarks?page=1 (O)

  * 포트번호가 다르지만, RFC 표준에서 http, https에 대한 포트는 생략이 가능하기 때문에 같은 출처로 본다.

* https://api.jinyoung.kr (X - host가 다르다.)

* https://jinyoung.kr:8080 (O)

  * 포트는 브라우저에 따라 정책이 다르다. IE의 경우를 제외하고 포트가 달라도 SOP가 인정된다.

  

### 시나리오



1.  Preflight Request

   * ``OPTIONS ``라는 메소드를 통해 header에 origin을 담아서 CORS 정책을 확인하는 예비요청을 보낸다. 

   * 서버는 ``Access-Control-Allow-Origin``  헤더에서 확인 후 OK 요청을 보낸다. 

   * 예비요청이 실패하면 브라우저에서 에러를 발생시킨다.

   * CORS는 **브라우저가 판단**하기 때문에 서버에서는 200대의 성공 코드를 반환한다.

   

2. Simple Request

   * 예비요청이 없고 본 요청에서 origin들을 비교한다. 

   * 요청 메소드는 **GET, HEAD, POST** 중 하나여야 한다.

   * header는 ``Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Width`` 만 사용할 수 있다.

   * ``Content-Type``에서 application/json이 허용되지 않는다.

     => 실질적으로 사용이 잘 안되는 이유



3. Credential Request

   * 인증 정보를 담아 보내는 요청

   * fetch 요청에서 ``(credentials: include)`` option을 줘서 cookie를 담아 보낸다.
   * ``Access-Control-Allow-Origin`` 에 ``*``(와일드카드)를 사용할 수 없다.
   * 응답헤더에는 ``Access-Control-Allow-Credentials: true``가 존재해야 한다.



### CORS 해결 방법

* 클라이언트 : web server에서 우회해서 요청을 날린다.
* 서버 : ``Access-Control-Allow-Origin``을 설정해준다. ex) express - cors 미들웨어 사용 