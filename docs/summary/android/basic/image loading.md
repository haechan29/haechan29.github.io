---
title: Image Loading
layout: default
parent: Basic
grand_parent: Android
nav_order: 6
---

## 고해상도 이미지의 로딩 방법은?
Glide, Picasso와 같은 이미지 로딩 라이브러리를 사용할 수 있습니다.<br/>

### Glide
- placeholder(): 이미지 로딩 중 보여줄 이미지를 설정<br/>
- thumbnail()을 통해 이미지가 로딩되는 동안 낮은 화질로 먼저 보여줄 수 있다.<br/>
- skipMemeoryCache()를 통해 메모리 캐싱 생략<br/>
- diskCacheStrategy(DiskCacheStrategy.NONE) 디스크 캐싱 생략<br/>

