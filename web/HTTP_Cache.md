## HTTP Cache

### Why?

네트워크를 통해 data를 fetch해오는 작업은 다른 작업에 비해 상대적으로 느릴 뿐더러 많은 비용을 요구한다.

* response size가 크면 브라우저와 서버 사이의 많은 왕복이 요구될 수 있다.
* 페이지 로딩이 길어질 수 있다.

웹 캐시는 특정 위치에 복사본을 저장하고 동일한 URL의 리소스 요청은 내부에 저장한 파일을 사용하여 빠르게 받아오기 위한 것이다.

웹 캐시는 Browser Cache, Proxy Cache, Gateway Cache가 있다. 그중 Browser Cache는 HTTP Header를 통해 사용할 수 있다.

관련 태그는 다음과 같다.

* Cache-Control

* ETag
* Last-Modified



### Cache-Control

요청과 응답 사이의 캐싱 옵션을 정하는데 사용된다.

Cache-Control: no-store와 같이 사용한다. 콤마로 구분해서 옵션을 중복해서 사용할 수 있다.

* no-store : 아무것도 캐싱하지 않음
* no-cache : 캐시를 하기 전에 서버에 재검증을 요청
* public : 공유 캐시에 저장
* private : 브라우저같은 특정 사용자 환경에만 저장
* max-age=3600 : 캐시 유효시간 설정
* stale-while-revalidate



### ETag

HTTP 컨텐츠가 바뀌었는지 검사할 수 있는 태그. 특정 문자열로 표현되며 ``If-None-Match`` 헤더와 함께 쓰인다. 

1. 브라우저는 최초 응답 시 받은 Etag 값을  ``If-None-Match`` 헤더에 포함시켜 페이지를 요청한다.
2. 서버는 요청 파일의 Etag 값을 ``If-Node-Match`` 값과 비교하여 리소스가 같은지 여부를 확인하고, 만약 같다면 304(Not modified) 코드를 반환한다.

3. 브라우저는 응답 코드가 304인 경우 캐시에서 페이지를 로드하고 200이라면 새로 다운받은 후 Etag 값을 갱신한다.



### Last-Modified

브라우저가 서버로 요청한 파일의 최종 수정 시간을 알려주는 헤더. 

1. 브라우저는 최초 응답 시 받은 Last-Modified 값을 ``If-Modified-Since`` 헤더에 포함시켜 페이지를 요청한다.
2. 서버는 요청 파일의 수정 시간을 ``If-Modified-Since``값과 비교하여 만약 같다면 304(Not modified) 코드를 반환한다.
3. 브라우저는 응답 코드가 304인 경우 캐시에서 페이지를 로드하고 200이라면 새로 다운받은 후 Modified 값을 갱신한다.







### Reference

* https://web.dev/http-cache/
* https://www.zerocho.com/category/HTTP/post/5b594dd3c06fa2001b89feb9
* https://developer.mozilla.org/ko/docs/Web/HTTP/Caching
* https://jjshun.tistory.com/59
* https://goodgid.github.io/REST-API/
* https://cyberx.tistory.com/9