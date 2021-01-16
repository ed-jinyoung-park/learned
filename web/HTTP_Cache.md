## HTTP Cache

### Why?

네트워크를 통해 data를 fetch해오는 작업은 다른 작업에 비해 상대적으로 느릴 뿐더러 많은 비용을 요구한다.

* response size가 크면 브라우저와 서버 사이의 많은 왕복이 요구될 수 있다.
* 페이지 로딩이 길어질 수 있다.

HTTP Cache는 완벽하진 않지만 효율적이고 모든 브라우저에서 제공되며, 작업이 간단하다.

보통 200, 301(다른 주소로 이동후 가져옴), 404(Not Found) 상태코드로 온 응답을 캐싱한다.

Cache는 request header와 response header의 조합으로 작동하며, 관련된 header는 다음과 같다.

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

서버는 클라이언트에서 받은 ETag를 확인하여 리소스가 같은지 여부를 확인하고, 만약 같다면 304(Not modified) 코드를 반환한다.



### Last-Modified

브라우저가 서버로 요청한 파일의 최종 수정 시간을 알려주는 헤더. 

![The request issued when the cache is empty triggers the resource to be downloaded, with both validator value sent as headers. The cache is then filled.](https://mdn.mozillademos.org/files/13729/Cache1.png)



### Reference

* https://web.dev/http-cache/
* https://www.zerocho.com/category/HTTP/post/5b594dd3c06fa2001b89feb9
* https://developer.mozilla.org/ko/docs/Web/HTTP/Caching

* https://jjshun.tistory.com/59