---
title: Strong/Weak Reference
layout: default
parent: Basic
grand_parent: Java, Kotlin
nav_order: 8
---

## 여러 가지 Reference
### Strong Reference
- 일반적인 참조 형태.<br/>
- 객체가 참조되는 동안에는 [GC] [1]에 의해 수집되지 않는다.<br/>

### Weak Reference
- Strong Reference와 다르게 GC에 의해 수집될 수 있다.<br/>
- Ex. WeakHashMap<sup>1</sup>, Listener<sup>2</sup>.<br/>
    ```kotlin
    exampleButton.setOnClickListener(object: View.OnClickListener {
        // 액티비티를 약하게 참조한다.
        val weakActivity = WeakReference(this@ExampleActivity)

        override fun onClick(view: View?) {
            val activity = weakActivity.get()
            activity?.let {
                // 액티비티의 멤버에 안전하게 접근한다.
            }
        }
    })
    ```
    <br/>

### Soft Reference
- 메모리가 부족해지면 GC에 의해 회수된다.<br/>
- 캐시와 같이 메모리에 민감한 구현에 사용된다.<br/>

### Phantom Reference
- 객체가 GC에 의해 회수되기 직전에 정리 작업을 수행할 기회를 제공한다.<br/>
    ```kotlin
    val queue = ReferenceQueue<Object>()
    var importantObject = Object()
    val phantomReference = PhantomReference<Object>(importantObject, queue)
   
    importantObject = null
            
    System.gc()
  
    val ref = queue.poll()
    ref?.let {
        // 정리 작업 수행. Ex. 리소스 해제.
    }
    ```
    <br/>

<sup>1</sup>키를 약한 참조로 저장한다. 즉, 키가 참조되지 않으면 해당하는 엔트리는 Map에서 삭제된다.<br/>
<sup>2</sup>Listener에서 외부 객체를 참조할 때는 약한 참조를 사용해야 한다.<br/>

[1]: /docs/summary/etc/garbage%20collection.html