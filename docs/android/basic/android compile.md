---
title: 안드로이드 앱의 컴파일 과정
layout: default
parent: Basic
grand_parent: Android
nav_order: 2
---

## 안드로이드 앱은 어떻게 컴파일되나요?
### 안드로이드 앱의 컴파일 과정
안드로이드 앱의 컴파일 과정은 여러 단계를 거칩니다. 이 과정은 크게 Java 소스 코드를 컴파일하여 바이트코드로 변환하는 과정, 바이트코드를 다시 안드로이드 플랫폼에서 실행 가능한 Dalvik Executable (DEX) 파일로 변환하는 과정, 그리고 이러한 DEX 파일들을 APK 파일 형식으로 패키징하는 과정으로 구분할 수 있습니다.<br/>

1. Java 소스 코드 컴파일링: 개발자가 작성한 Java 소스 코드는 Java 컴파일러(javac)에 의해 바이트코드(.class 파일)로 컴파일됩니다. 이 바이트코드는 Java 가상 머신(JVM)에서 실행될 수 있으며, 안드로이드 개발에서는 이후 단계에서 더 처리됩니다.<br/>
2. DEX 변환: Android SDK에 포함된 dx 도구나 Android Studio의 빌드 시스템은 .class 파일들을 Dalvik Executable 형식, 즉 .dex 파일로 변환합니다. DEX 파일 포맷은 안드로이드 플랫폼에 최적화되어 있으며, JVM 바이트코드보다 메모리 효율성과 실행 속도 면에서 우수한 성능을 제공합니다. Android Runtime (ART) 또는 이전의 Dalvik 가상 머신에서 실행됩니다.<br/>
3. APK 패키징: .dex 파일과 애플리케이션의 리소스 파일들(이미지, 문자열 등)은 APK(Android Package) 파일로 패키징됩니다. 이 과정은 aapt (Android Asset Packaging Tool) 도구를 사용하여 수행되며, 결과물인 APK 파일은 안드로이드 디바이스에 설치되어 앱으로 실행됩니다.<br/>
4. 서명 및 최적화: APK 파일은 배포 전에 개발자의 키로 서명되어야 하며, 때로는 zipalign 도구를 사용하여 APK 파일을 최적화하여 안드로이드 디바이스에서의 앱 실행 성능을 향상시킬 수 있습니다.<br/>

### Dalvik vs ART
DEX 파일을 실행하는 안드로이드 최적화 가상 머신입니다.<br/> 

- [Dalvik] [1]은 JIT 컴파일을 사용하여 애플리케이션을 실행할 때마다 일정한 시간이 소요된다.<br/>
- [ART] [2]는 AOT 컴파일 방식을 사용하여 실행 속도가 빠르고, 시스템 효율성이 높다.<br/>
- ART는 Android 4.4 KitKat 버전에서 처음 소개되어, 이전에 사용되던 Dalvik 가상 머신을 대체했다.<br/>

### JIT vs AOT
프로그램 코드를 실행 가능한 기계어 코드로 변환하는 두 가지 다른 접근 방식입니다.<br/>

1. JIT (Just-In-Time) 컴파일
   - JIT 컴파일러는 프로그램이 실행되는 동안 실시간으로 바이트코드나 중간 언어를 기계어 코드로 변환한다.<br/>
   - 실행 시간에 필요한 코드 부분만을 선택적으로 컴파일한다.<br/>
   - 초기 컴파일에 드는 시간이 짧다.<br/>
   - 실행 속도가 느려질 수 있다.<br/>
   <br/>

2. AOT (Ahead-Of-Time) 컴파일
   - AOT 컴파일러는 프로그램을 설치할 때 전체 코드를 기계어 코드로 미리 변환한다.<br/>
   - 프로그램의 실행 속도가 JIT 방식에 비해 빠르다.<br/>
   - 설치 시간이 길어지고 애플리케이션의 초기 크기가 커질 수 있다.<br/>
   <br/>

[1]: https://brunch.co.kr/@mystoryg/81
[2]: https://brunch.co.kr/@mystoryg/82
