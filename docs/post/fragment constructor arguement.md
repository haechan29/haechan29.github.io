---
title: Fragment에 값 전달하기 
layout: default
parent: Post
---

## Fragment에 값 전달하기
### 미리 보는 결론
- Android는 Fragment에 값을 직접 전달하기를 권장하지 않는다.<br/>
- Fragment에 값을 직접 전달하기 보다는 (1) **ViewModel을 통해 데이터를 공유**하거나, (2) **Fragment로부터 이벤트를 전달받는 방식**을 사용하자.<br/><br/>

### Fragment에 값 전달하기가 어려운 이유
1. Fragment는 재생성<sup>1</sup>될 때 반드시 기본 생성자를 사용한다.<br/>
   - 만약 Fragment가 재생성될 때 기본 생성자가 존재하지 않으면 `NoSuchMethodException`이 발생한다.<br/><br/>

2. Fragment는 기본적으로 재생성에 취약하다.<br/>
    - 재생성 과정에서 따로 저장하지 않은 [데이터는 일부 유실되고] [Saving State], 자동으로 복원되지 않는다.<br/>
    - Fragment의 지역 변수 등 초기화되지 않은 데이터가 재생성 과정에서 `NullPointerException`과 같은 예외를 일으킨다.<br/><br/>

3. `Bundle`, `FragmentFactory`와 같이 Fragment 생성 시에 값을 전달할 수 있는 방법이 존재하지만, 제한적이며 단순히 생성자 인자를 전달하는 것 치고는 굉장히 번거롭다.<br/><br/>

### 그럼에도 불구하고 Fragment에 값을 전달하는 방법
1. `Bundle` 이용하기
   - Fragment 생성 시에 `setArgument()` 메서드를 사용한다.<br/>
   - 전달할 수 있는 인자 타입은 Int, String, Parcelable 등으로 제한적이다.<br/><br/>

2. `FragmentFactory` 사용하기
   - `FragmentFactory#instantiate()`을 Override한 후 `FragmentManager#setFragmentFactory()`를 호출한다.<br/>
   - `FragmentFactory#instantiate()`를 Override하는 시점에 생성자 인수 값이 고정되어야 한다.<br/><br/>

3. 현실적인 타협안
   - 재생성시 Fragment를 없앤다. (`FragmentManager#popBackStack()`을 호출한다)<br/>
   - Host Activity의 [재생성을 막는다] [Restrict Activity Recreateion]. (`Manifest.xml`을 통해 Activity 별로 Configuration Change를 제한할 수 있으나, *권장되지 않는 방식이다*)<br/><br/>

### 더 나은 방법
1. ViewModel을 사용한다.
   - 쉽고 간편하다. 말이 더 필요 없다.<br/><br/>

2. Fragment로부터 이벤트를 전달받는다.
   - 예를 들어 FragmentDialog의 경우 Positive, Negative 버튼의 클릭을 Activity가 감지하고, 처리하도록 할 수 있다(Observer 패턴).<br/><br/>  

<sup>1</sup>화면 회전 등에 의해 LifecycleOwner의 생명 주기가 파괴되고 다시 생성되는 것.<br/>

[Saving State]: https://developer.android.com/guide/fragments/saving-state
[Restrict Activity Recreateion]: https://developer.android.com/guide/topics/resources/runtime-changes#restrict-activity