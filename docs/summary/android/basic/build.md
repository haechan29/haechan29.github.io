---
title: 안드로이드 앱의 빌드 과정
layout: default
parent: Basic
grand_parent: Android
nav_order: 10
---

## 안드로이드 앱은 어떻게 빌드되나요?
### 안드로이드 앱의 빌드 과정
1. 컴파일: Java 소스 코드는 javac에 의해 바이트 코드(.class 파일)로 [컴파일] [1]된다.<br/>
2. 변환: class 파일을 dex<sup>1</sup> 파일로 변환한다.<br/>
3. 패키징: dex 파일과 리소스 파일은 AAPT<sup>2</sup>를 통해 APK<sup>3</sup> 파일로 패키징된다.<br/>
4. 서명 및 최적화: APK 파일은 배포 전에 개발자의 키로 서명되어야 한다. [zipalign] [2] 등의 도구를 사용하여 APK 파일을 최적화한다.<br/><br/>

<sup>1</sup>Dalvik Executable. 안드로이드 플랫폼에 최적화되어 있다. [ART 또는 Dalvik 가상 머신에서 실행된다.] [3]<br/>
<sup>2</sup>Android Asset Packaging Tool.<br/>
<sup>3</sup>Android Package. Android의 실행 파일 형식.<br/>

[1]: /docs/summary/os/basic/build.html
[2]: https://developer.android.com/tools/zipalign
[3]: dalvik%20vs%20art.html