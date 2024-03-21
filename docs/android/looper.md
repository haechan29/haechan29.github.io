---
title: Looper
layout: default
parent: Android
nav_order: 7
---

## Looper란?
### Looper
- 스레드가 메시지 루프를 통해 작업을 처리할 수 있도록 하는 메커니즘<br/>
- 안드로이드 애플리케이션의 메인 스레드는 기본적으로 Looper를 사용하여 사용자 인터페이스 이벤트(예: 터치 이벤트, 버튼 클릭 등)를 처리합니다.<br/>
- Looper는 특정 스레드에 연결되어 그 스레드에 메시지 루프를 제공합니다. 이 메시지 루프는 MessageQueue에서 작업(Message, Runnable 객체)을 차례로 가져와 순차적으로 실행합니다.<br/>
- 안드로이드의 메인 스레드는 Looper가 기본적으로 설정되어 있고, 백그라운드 스레드에서는 Looper.prepare()을 통해 Looper을 설정할 수 있습니다.<br/>

### Handler
- UI 스레드(메인 스레드)와 백그라운드 스레드 간의 통신을 용이하게 하는 클래스<br/>
- 특정 Looper에 연결되어 있으며, 해당 Looper의 메시지 큐(MessageQueue)에 메시지를 보내거나, 특정 시간이 지난 후에 코드를 실행하는 등의 작업 스케줄링을 할 수 있습니다.<br/>

### Runnable vs Message
Handler에 의해 실행되는 작업입니다.<br/>
- Runnable 객체는 생성과 동시에 실행 내용이 run() 메서드를 통해 작성됩니다.<br/>
- Message 객체는 Handler 내부의 handleMessage()를 통해 실행됩니다. 따라서 Message를 처리하는 방식에 따라 Handler의 서브클래스를 생성하여 Message를 일관성 있게 처리할 수 있습니다.<br/>
