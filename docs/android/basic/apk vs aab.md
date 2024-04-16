---
title: APK vs AAB
layout: default
parent: Basic
grand_parent: Android
nav_order: 10.2
---

## AAB vs APK
### APK(Android Package)
- 안드로이드 앱을 배포하는 기존의 포맷.
- 앱의 모든 코드와 리소스를 하나의 파일로 패키징합니다.
- 개발자는 APK 파일을 생성하고, 이를 사용자가 다운로드하여 직접 설치하거나 Google Play 스토어를 통해 배포할 수 있습니다.

### AAB(Android App Bundle)
- Google Play의 새로운 배포 포맷.
- 주된 목적은 앱을 사용자에게 최적화하여 앱의 크기를 줄이는 것입니다. 이를 통해 다운로드 시간, 설치 시간, 앱의 저장 공간 사용량이 감소합니다.
- 개발자가 AAB 파일을 Google Play에 업로드하고, 사용자가 Google Play에서 앱을 다운로드할 때 디바이스의 구성(화면 크기, CPU 아키텍처 등)에 맞게 필요한 코드와 리소스만 포함한 APK를 동적으로 생성합니다.

### 주요 차이점
- 배포 방식: AAB는 Google Play를 통해서만 배포될 수 있으며, APK는 Google Play 외에도 다양한 방식으로 직접 배포할 수 있습니다.
- 파일 크기: AAB는 사용자의 디바이스에 맞춰 최적화된 APK를 생성하여 배포하기 때문에, APK에 비해 다운로드 크기와 설치 후 차지하는 공간이 더 작습니다.
- 개발자 편의성: AAB는 개발자가 [여러 APK를 관리할 필요 없이] [1] 하나의 번들로 앱을 관리할 수 있게 해줍니다.

[1]: https://trend21c.tistory.com/2029
