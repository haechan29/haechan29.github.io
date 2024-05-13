---
title: REST API
layout: default
parent: HTTP
grand_parent: Network
nav_order: 4
---

## REST API란?
### REST API
- Representational State Transfer 아키텍처 모델을 준수하는 API.<br/>
- 아래의 요구사항을 만족하는 API.<br/>
    1. Uniform-Interface: 리소스에 대한 요청이 균일한 인터페이스를 가지는 것.<br/>
        - Identification of resources: url을 통해 자원을 식별하는 것.<br/>
        - Manipulation of resources through representations: HTTP 메서드 등을 통해 자원을 조작하는 것.<br/>
        - Self-descriptive messages: 메시지가 host, MIME 타입 등 통신을 위해 필요한 정보를 모두 갖는 것.<br/>
        - HATEOAS: Hypermedia as the Engine of Application State, Application의 상태가 Hyperlink에 의해 전이되는 것.<br/><br/>

    2. Stateless: 통신 과정에서 정보를 저장하지 않는다. HTTP를 사용하면 자동으로 지원된다.<br/>
    3. Cacheable: 캐싱 가능. HTTP를 사용하면 자동으로 지원된다.<br/>
    4. Client-Server 구조: 클라이언트와 서버가 서로 독립적인 구조를 가져야 한다. HTTP를 사용하면 자동으로 지원된다.<br/>
