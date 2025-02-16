---
title: Fragment
layout: default
parent: Basic
grand_parent: Android
nav_order: 2
---

## Fragment란?
### Fragment
- 다양한 해상도의 화면을 지원하기 위한 UI 요소.<br/>
- 단독으로 실행될 수 없고 Activity, Fragment 등의 UI 요소에서 실행되어야 한다. <br/>

### 특징
- 자체적인 레이아웃을 가진다. 인플레이트된 뷰 트리는 호스트 뷰에 연결된다.<br/>
- 호스트와 독립적인 수명 주기를 가진다.<br/>
- UI를 표현하기 위한 루트 뷰를 가진다.<br/>

### 사용법
- 호스트의 레이아웃에 Fragment Container<sup>1</sup>을 선언한다.<br/>
- ``name`` 속성에 Fragment의 클래스 이름을 설정한다.<br/>

### Navigation
- Fragment의 Transition, 데이터 전달, Animation 등을 지원한다.<br/>
- ``name`` 속성에 NavHostFragment를 설정하고, NavGraph<sup>2</sup>를 등록하여 사용한다.<br/><br/>

<sup>1</sup>FragmentContainerView<sup>3</sup>, Fragment, FrameLayout 등.<br/>
<sup>2</sup>``popUpTo``는 Transition 시에 Target 프래그먼트가 나올때까지 백스택에서 제거한다. ``popUpToInclusive``를 true로 설정하면 Target 프래그먼트까 제거한다.<br/>
<sup>3</sup>Fragment, FrameLayout를 대체하기 위한 뷰.<br/>