---
title: 이미지 포맷
layout: default
parent: Etc
grand_parent: Summary
nav_order: 1.1
---

## 여러 이미지 포맷은 언제 사용될까?
### JPEG
- Joint Photographic Experts Group.<br/>
- 래스터 이미지<sup>1</sup>.<br/>
- 파일 크기가 중요하고 투명도가 필요 없는 이미지에 주로 사용.<br/>
- **손실 압축** 형식. 최대 1/10까지 용량을 줄일 수 있음.<br/>
- 비슷한 픽셀을 병합. 일부 데이터가 영구적으로 손실된다.<br/>

### PNG
- Portable Network Graphics.<br/>
- 래스터 이미지.<br/>
- 화질을 유지하고 싶거나 투명도가 필요한 경우에 주로 사용.<br/>
- **무손실 압축** 형식.<br/>
- 투명도를 지원한다.<br/>

### [WebP] [2]
- 웹에서 사용하기 위해 설계되었다. JPEG, PNG, GIF와 같은 기존 이미지 포맷에 비해 우수한 압축 기술을 제공한다.<br/>
- 손실 압축시 용량이 JPEG에 비해 약 30% 더 작다.<br/>
- 무손실 압축시 용량이 PNG에 비해 약 25% 더 작다.<br/>
- 투명도를 지원한다.<br/>

<br/>

<sup>1</sup>[래스터 이미지] [1]: 작은 점을 무수히 여러 번 찍어 만들어낸 이미지.<br/>

[1]: raster%20vs%20vector.html
[2]: https://developers.google.com/speed/webp?hl=ko
