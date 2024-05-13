---
title: Fragment Lifecycle
layout: default
parent: Basic
grand_parent: Android
nav_order: 2.1
---

## Fragment의 생명 주기는 어떻게 구성될까?
### Fragment의 생명 주기<sup>1</sup>
1. onAttach(): Fragment가 호스트에 부착된다.<br/>
2. onCreate(): Fragment가 생성된다.<br/>
3. onCreateView(): Fragment의 레이아웃을 인플레이트한다<sup>2</sup>.<br/>
4. onViewCreated(): 인플레이트된 뷰를 통해 추가 작업을 수행한다<sup>3</sup>.<br/>
5. onStart(): Fragment가 화면에 보이기 시작한다.<br/>
6. onResume(): Fragment가 화면 최상단에 보이고, 사용자와 상호작용한다.<br/>
7. onPause(): Fragment가 포커스를 잃거나 멀티 윈도우 모드에 진입한다.<br/>
8. onStop(): Fragment가 완전히 보이지 않게 된다. Fragment 백스택으로 이동한다.<br/>
9. onDestroyView(): Fragment가 백스택에 있는 동안 Fragment 내부의 뷰가 소멸된다.<br/>
10. onDestroy(): Fragment가 소멸된다.<br/>
11. onDetach(): Fragment가 호스트와 분리된다.<br/><br/>

<sup>1</sup>Fragment는 내부적으로 View를 가지고, 이들은 각각 [다른 생명주기를 갖는다.] [2] 내부의 View과 관련된 부분을 제외하면 Activity의 생명 주기와 거의 유사하다.<br/>
<sup>2</sup>UI를 갖지 않는 [Headless Fragment] [3]의 경우 null을 반환하면 된다. 이 경우 getViewLifecycleOwner()은 null을 반환한다.<br/>
<sup>3</sup>뷰의 초기 상태 설정, LiveData 구독, RecyclerView 어댑터 설정 등. [해당 작업은 onCreateView()애서 수행하지 않는 것이 좋다.] [1]<br/>
<sup>4</sup>Fragment 내부의 뷰에 대한 참조를 해제해야 한다<sup>4</sup>. 뷰 바인딩을 사용하는 경우 바인딩 객체에 대한 참조만 해제하면 된다.<br/>

[1]: https://developer.android.com/reference/androidx/fragment/app/Fragment#onCreateView(android.view.LayoutInflater,android.view.ViewGroup,android.os.Bundle)
[2]: https://developer.android.com/guide/fragments/lifecycle?hl=ko
[3]: https://devatom.tistory.com/5
