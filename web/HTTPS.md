## HTTPS

> HTTP + TLS(SSL). HTTP 위에 SSL을 얹은 프로토콜



### Why?

1. 개인정보 보호

   데이터를 암호화해서 개인정보를 보호한다.

2. 무결성

   중간자 공격을 막아 데이터가 변형되지 않았음을 보장한다.

3. 식별

   SSL 인증서를 통해 발신자를 확인할 수 있으며, 예상한 수신자에게 정확히 연결해준다.

여기서의 핵심은 데이터를 **암호화**한다는 것이다.



### SSL (TLS)

> Secure Sockets Layer

넷스케이프에 의해 작성된 보안을 위한 프로토콜. IETF(Internet Engineering Task Force)에 제어권을 넘긴 후 SSL 3.1 버전이 TLS 1.0으로 바뀐다. 현재는 TSL 1.3으로 쓰이고 있다.

SSL 인증서에는 다음과 같은 정보가 포함되어 있다.

1. 서비스의 정보 (인증서를 발급한 CA, 서비스 도메인)
2. 서버측 공개키



SSL을 사용하려면 지정된 CA 기관에서 인증서를 받아야 한다.



### SSL 전달방식

암호화된 데이터를 전달하기 위해 **공개키와 대칭키 방식을 혼합해서** 사용한다. 

1. 클라이언트가 서버에 접속한며 랜덤데이터를 전송한다. (ex - Client Hello)
2. 서버가 랜덤데이터에 대한 응답과 인증서를 같이 보낸다. (ex- Server Hello)
3. 클라이언트(브라우저)에서는 서버가 건네준 인증서가 CA에서 발급된 것인지 확인하고 공개키로 인증서를 복호화한다.
4. 클라이언트에서는 각각의 랜덤 데이터를 가지고 pre master secret값을 만들어낸다.(대칭키)
5. pre master secret 값을 서버의 공개키로 암호화하고 서버에 보낸다.
6. 서버는 비공개키로 pre master secret 값을 복호화한다. 
7. 서버와 클라이언트는 pre master secret 값을 master secret 값으로 만들고 이 값을 session key라고 한다.
8. 서버와 클라이언트는 대칭키(session key)방식으로 이를 암호화하고 주고받는다. 세션이 끝나기 전까지 보호받는다.





### Reference

* https://howhttps.works/ko/
* https://dodonam.tistory.com/74