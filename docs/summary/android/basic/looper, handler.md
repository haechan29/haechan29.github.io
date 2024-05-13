---
title: Looper, Handler
layout: default
parent: Basic
grand_parent: Android
nav_order: 7
---

## Looper와 Handler
### Looper
- 스레드가 메시지 루프를 사용할 수 있게 한다.<br/>
- 특정 스레드에 연결되어 MessageQueue에서 작업<sup>1</sup>을 차례로 가져온다.
- 메인 스레드를 제외한 스레드는 기본적으로 Looper을 갖지 않는다. Looper.prepare()을 통해 Looper을 생성할 수 있다.<br/>
- 메인 스레드는 기본적으로 Looper를 갖고, 이를 통해 사용자 인터페이스 이벤트(예: 터치 이벤트, 버튼 클릭 등)를 처리한다.<br/>
- Looper#getMainLooper()는 메인 스레드의 루퍼를, Looper#myLooper()는 현재 스레드의 루퍼를 반환한다.<br/>

### Handler
- 스레드의 메시지 큐에 작업을 전송하거나 메시지 큐로부터 전달받은 작업을 처리한다.<br/>
- handleMessage()를 통해 Message 객체를 정해진 방법으로 처리하거나 post(), postDelayed()를 통해 Runnable 객체를 싦행한다.<br/>
- 특정 Looper에 연결되어 있다.<br/><br/>

<sup>1</sup>Message 또는 Runnable 객체.<br/>