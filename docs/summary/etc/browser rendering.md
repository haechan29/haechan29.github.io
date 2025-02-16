---
title: 웹 브라우저의 렌더링 과정
layout: default
parent: Etc
grand_parent: Summary
nav_order: 14
---

## 웹 사이트는 어떻게 그려질까?
### 웹 브라우저의 렌더링 과정
1. URL 입력<br/>
    - 사용자가 웹 브라우저에 URL을 입력한다.<br/>
    - 브라우저는 해당 서버에 HTTP 요청을 보낸다.<br/>
    - 서버는 HTML 문서를 반환한다.<br/><br/>

2. HTML 파싱 & CSS 파싱<br/>
    - HTML 파서를 통해 DOM 트리<sup>1</sup>를 구성한다.<br/>
    - CSS<sup>2</sup> 파서를 통해 CSSOM 트리를 구성한다.<br/><br/>

3. 렌더 트리 구성<br/>
    - DOM 트리와 CSSOM 트리를 합쳐 렌더 트리를 구성한다.<br/>
    - 렌더 트리는 페이지를 그리는 데 필요한 모든 요소와 스타일 정보를 포함한다.<br/>
    - 실제 화면에 표시되지 않는 요소는 포함되지 않는다(Ex. display: none 속성을 가진 요소).<br/><br/>

4. 레이아웃 처리<br/>
    - 렌더 트리를 기반으로 각 요소의 정확한 위치와 크기를 계산한다.<br/>
    - 각 요소는 상대적인 위치를 가진다.<br/><br/>

5. 렌더 레이어 생성<br/>
    - 다른 요소들과 독립적으로 렌더링되어야 하는 요소(Ex. CSS의 position: fixed 속성이나 opacity 속성을 가진 요소)를 위한 별도의 레이어를 생성한다.<br/>
    - 성능 최적화와 복잡한 시각적 효과 구현에 유리하다.<br/><br/>

6. 페인팅<br/>
    - 픽셀로 화면에 그린다.<br/>
    - 텍스트, 색상, 이미지 등이 화면에 표시된다.<br/><br/>

7. 합성<br/>
    - 렌더 레이어를 합성하여 최종 이미지를 형성한다.<br/><br/>

<sup>1</sup>Document Object Model 트리. HTML 문서의 구조를 표한한다.<br/>
<sup>2</sup>Cascading Style Sheets. 스타일 정보를 담고 있다.<br/>