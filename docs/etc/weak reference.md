---
title: Weak Reference
layout: default
parent: Etc
nav_order: 11
---

## WeakReference란?
### WeakReference
WeakReference는 일반적인 강한 참조(strong reference)와 다르게, 가비지 컬렉터에 의해 수집(삭제)될 수 있도록 허용합니다.<br/>

### 예시
- WeakHashMap: WeakHashMap의 키는 약한 참조로 저장됩니다. 즉, 특정 키를 참조하는 다른 곳이 없을 경우 해당 키-값 쌍을 컬렉션에서 제거합니다.<br/>
- Listener: 안드로이드에서 뷰의 리스너가 외부의 뷰, 액티비티 등을 참조하는 경우 생명주기가 끝난 후에도 제거되지 않을 수 있습니다.<br/>
<br/>

### 또다른 Reference
- Soft Reference: 메모리가 부족해지면 가비지 컬렉터에 의해 회수됩니다. 따라서 캐시와 같은 메모리에 민감한 구현에 유용합니다.<br/>
- Phantom Reference: 객체가 가비지 컬렉터에 의해 회수되기 직전에 정리 작업을 수행할 기회를 제공합니다.<br/>
  PhantomReference의 생성자는 객체와 ReferenceQueue를 인자로 받는데, 객체가 가비지 컬렉터에 의해 수집되면 참조 큐에 추가됩니다. 참조 큐를 폴링하여 객체에 대한 정리 작업을 수행할 수 있습니다.<br/>
  <br/>
  Ex
  
  ```java
  public class PhantomReferenceExample {
  public static void main(String[] args) throws InterruptedException {
  // 객체와 참조 큐 생성
  ReferenceQueue<Object> queue = new ReferenceQueue<>();
  Object importantObject = new Object();
  PhantomReference<Object> phantomReference = new PhantomReference<>(importantObject, queue);
  
          importantObject = null;
  
          System.gc();
  
          PhantomReference<?> ref = (PhantomReference<?>) queue.poll();
          if (ref != null) {
              // 정리 작업 수행
              // 예: 리소스 해제 등
          }
      }
  }
  ```
