# Local Storage, Session Storage, Cookie의 차이

### Web Storage(Local, Session) VS Cookie

**Cookie**

- client와 server 모두에서 접근 가능하다.

  ⇒ cookie는 네트워크 요청시 서버에 전송된다.

- 4KB data까지만 허용된다.

- 만료시간을 설정할 수 있다.
  - session cookie - 세션 종료시 사라진다.
  - persistent cookie - 만료시간이 지나면 사라진다.

**Web Storage**

- Web storage는 client에서 데이터를 저장할 수 있는 공간이다.

  ⇒ 네트워크 요청시 서버에 전송되지 않는다.

- Web storage는 5MB까지 허용된다.(브라우저에 따라 다름)
  ⇒ 네트워크 요청에 포함되지 않기 때문에 쿠키보다 더 많은 용량을 보유할 수 있다.

- 만료시간이 따로 없다.
  - session storage는 페이지 세션 종료시 사라진다.
  - local storage는 따로 지워주지 않는 한 지속된다.

### Local Storage vs Session Storage

**Local Storage**

- Local Storage는 브라우저에서 별도로 지우지 않는 한 계속 남아있다.(브라우저를 다시 켜도 남아있다)
- Local Storage는 같은 브라우저의 다양한 탭에서 공유된다.

**Session Storage**

- Session Storage는 브라우저 또는 탭이 닫힐 때까지만 데이터가 남아있다.(페이지 세션이 끝나면 사라진다)
