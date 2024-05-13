---
title: Dalvik vs ART
layout: default
parent: Basic
grand_parent: Android
nav_order: 10.1
---

## Dalvik vs ART
### Dalvik
- 주로 [JIT 컴파일] [1]하며 가끔씩 인터프리터를 사용한다.<br/>
- [dexopt를 통해 dex 파일을 플랫폼 최적화하여 odex 파일으로 변환한다.] [2]<br/>


### ART
- [AOT 컴파일] [1]과 JIT 컴파일을 [같이 사용한다] [3]<sup>1</sup>.<br/>
- [dex2oat를 통해 dex 파일을 odex 파일로 변환한 후에 oat 파일로 다시 변환한다.] [4]<br/>
- Android 4.4 KitKat 버전에서 처음 소개되어, 이전에 사용되던 Dalvik 가상 머신을 대체했다.<br/><br/>

<sup>1</sup>APK 파일은 AOT 컴파일 없이 설치되고 실행 시에 JIT 컴파일한다. 이후 유휴 상태에서 충전 중일때 자주 사용되는 코드를 AOT 컴파일한다. 이후 컴파일된 내용을 기반으로 실행된다.<br/>

[1]: /docs/summary/etc/jit%20vs%20aot.html
[2]: https://brunch.co.kr/@mystoryg/81
[3]: https://source.android.com/docs/core/runtime/configure?hl=ko
[4]: https://brunch.co.kr/@mystoryg/82

