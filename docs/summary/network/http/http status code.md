---
title: HTTP 상태 코드
layout: default
parent: HTTP
grand_parent: Network
nav_order: 3
---

## HTTP 상태 코드의 의미는?
### HTTP 상태 코드
1. 1xx: 정보 응답<br/>
    - 100(Continue): 클라이언트는 요청을 계속 해야함.<br/>
    <br/>
   
2. 2xx: 성공<br/>
    - 200(OK): 요청이 성공적으로 처리됨.<br/>
    - 201(Created): 요청이 성공적으로 처리되어 새로운 리소스가 생성됨.<br/>
    - 204(No Content): 요청은 성공적이지만, 전송할 내용이 없음.<br/>
    <br/>
   
3. 3xx: 리다이렉션<br/>
    - 301(Moved Permanently): 요청한 리소스의 URI가 변경되었음.<br/>
    - 302(Found): 요청한 리소스가 일시적으로 다른 위치로 이동했음.<br/>
    - 304(Not Modified): 캐시된 리소스가 여전히 유효함.<br/>
    <br/>

4. 4xx: 클라이언트 오류<br/>
    - 400(Bad Request): 서버가 요청을 이해하지 못함.<br/>
    - 401(Unauthorized): 인증되지 않은 클라이언트.<br/>
    - 403(Forbidden): 서버가 요청을 거부함.<br/>
    - 404(Not Found): 요청받은 컨텐츠를 찾을 수 없음.<br/>
    - 408(Request Timeout): 요청 시간이 초과됨.<br/>
    <br/>

5. 5xx: 서버 오류<br/>
    - 500(Internal Server Error) : 서버에 오류가 있음.<br/>
    - 501(Not Implemented): 서버가 요청 메소드를 지원하지 않음.<br/>
    - 502(Bad Gateway): 게이트웨이 또는 프록시 서버에 오류가 생겼음.<br/>
    - 503(Service Unavailable): 서버가 과부하, 유지보수 등으로 인해 일시적으로 요청을 처리할 수 없음.<br/>
    <br/>