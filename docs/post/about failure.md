---
title: 실패에 관하여
layout: default
parent: Post
date: 2025-01-03
---

## 실패에 관하여
얼마 전 API 실패 처리를 누락하는 바람에 앱의 30만 유저에게 망가진 UI를 보여주고 말았다. (무한 스켈레톤!)<br/>
친절한 상사님께서는 실수는 병가지상사라는 재밌는 표현으로 위로해주셨지만, 실패 처리에 관한 교훈을 뼈저리게 느꼈다. (왜 플레이스토어 심사는 3일씩 걸리는가 ㅠㅠ)<br/><br/>

내친 김에 오늘은 여러 종류의 실패와 처리 방법에 대한 글을 적어보려고 한다.<br/><br/>

### 실패한 것과 하지 않은 것은 다르다.
프런트엔드 개발자의 흔한 고민은 초기값 설정이다. 비동기 작업(보통은 API 호출)을 통해 값을 얻어와야 하니 초기값을 무엇으로 두어야 하는지, 비동기 작업 실패는 어떻게 처리해야 할지 항상 애매하다.<br/><br/>

1년차 개발자인 현재는 초기값은 null, 실패는 Exception 반환으로 처리하고 있다.<br/>
null은 사람마다 받아들이는 의미가 다르겠지만 일반적으로 `없음`, `하지 않았음`을 나타낸다고 생각한다. 즉, 값이 설정되기 전에는 값이 없다는 의미로 null을 사용하는 것이다.<br/>
한편 값을 받아오지 못한 경우에는 Exception을 반환하도록 하는 편인데, 비정상적인 상황이라는 의미와 그 이유(`Throwale`.`message`를 활용하여)를 표현할 수 있고, Kotlin의 `runCatching`을 활용하여 성공/실패를 가독성 좋게 표현할 수 있으며, Kotlin에서는 `throw Exception` 표현이 Nothing 타입이기 때문에 메서드의 반환형에 얽매일 필요가 없어진다.<br/>
실패했음을 의미하는 플래그(또는 합의된 값)을 사용하거나 억지로 null을 반환할 필요가 없으니 얼마나 편리한가?<br/><br/>

### 실패를 실패로 두지 않는다.
모바일 개발자인 나는 플레이스토어와 앱 스토어같은 플랫폼 사업자들의 옥죄어 오는 손길을 느낀다. Android의 경우 버전에 따라 권한, 백그라운드 동작, 유저 정보 관리 등 하루가 다르게 정책이 촘촘해지고 있는데, 이에 따라 분기점도 늘고 있다.<br/><br/>

권한은 그 중에서도 가장 민감하다. `핵심 기능`이라는 주관적인 기준에 따라 허용 여부가 결정되기도 하고, 자칫 잘못하면 제재를 받을 수 있다. 그렇기에 유저에게 은밀하면서도 정직하게 권한 허용을 유도하기 위해 신경을 쓰는데, 권한 거부는 자칫 관심이 소홀해질 수 있는 시나리오다. (ex. 설마 거부하겠어? 이거 거부할거면 우리 앱 왜 써?)<br/><br/>

유저가 권한을 거부하더라도 핵심 권한이 아니라면 우회로를 생각해보자. 예를 들어 스타벅스 앱에서 주문할 매장 선택하기 버튼을 누르면 위치 권한을 요구하는데, 거부하면 위치 정보 접근이 허용되지 않았다며 매장명을 가나다 순으로 안내한다.<br/><br/>

구글과 친해지는 것도 하나의 방법이다. 요즘 만보기 앱이 늘면서 다양한 앱이 걸음수를 세어 주는데, 구현 방식은 다양하다. 하드웨어 센서를 이용할 수도 있고(핸드폰 끄면 초기화!), GoogleFit API를 사용할 수도 있다(구글 로그인 필수).<br/>
핸드폰이 언제 꺼질까 걱정하며 5분마다 걸음수를 서버로 보낼 것인가? 아니면 유저가 구글 아이디가 있고, 구글에 우호적이기만을 바라며 앱에 필요도 없는 구글 로그인을 강요할 것인가?<br/><br/>

이에 대해 구글이 제시하는 좋은 방법이 있다. [Local Recording API][1]를 사용하면 구글 로그인 없이도 걸음수를 얻어올 수 있다. 여전히 신체 활동 권한은 필요하고, 저장 기간도 최대 10일이지만 이만하면 만보기로는 충분하다.<br/><br/>

### 문제가 많으면 방법은 더 많다.
중국의 격언이라고 한다. 어쩌면 개발자(엔지니어)는 문제를 가장 많이 만나는 사람들이 아닐까 싶다. 옆에 있는 사람들을, 나 자신을 다독여가며 실패를 잘 넘어가보자.

[1]: https://developer.android.com/health-and-fitness/guides/recording-api?hl=ko