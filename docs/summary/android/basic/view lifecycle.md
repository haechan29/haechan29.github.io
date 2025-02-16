---
title: View Lifecycle
layout: default
parent: Basic
grand_parent: Android
nav_order: 3
---

## View의 생명 주기는 어떻게 구성될까?
### View의 생명 주기
1. constructor(): 뷰의 인스턴스를 생성.<br/>
2. onFinishInflate(): XML을 통해 뷰가 인플레이트된 후 호출된다.<br/>
3. onAttachedToWindow(): 뷰가 윈도우에 붙을 때 호출된다.<br/>
4. onMeasure(): 뷰의 크기를 결정한다<sup>1</sup>.<br/>
5. onLayout(): onMeasure()을 통해 결정된 크기를 바탕으로 뷰의 위치를 결정한다.<br/>
6. onDraw(): Canvas를 사용하여 그림을 그린다.<br/>

### View 다시 그리기
- invalidate(): onDraw()부터 재시작한다. **뷰의 크기 변화 없이** 글자나 색상 등의 속성이 변경되어 다시 그려야할때 호출한다.<br/>
- requestLayout(): onMeasure()부터 재시작한다. **뷰의 크기가 변화하는 경우 호출**한다.<br/><br/>

<sup>1</sup>자식 뷰를 포함하여 얼마나 많은 공간을 필요로 하는지 계산한다. 부모 뷰로부터 받은 MeasureSpec<sup>2</sup>을 기반으로 계산이 이루어진다. 각 뷰는 setMeasuredDimension() 메서드를 통해 자신의 크기를 결정한다.<br/>
<sup>2</sup>자식 뷰의 너비 또는 높이에 대한 요구 사항. 크기와 모드로 구성되며, 세 가지 모드가 있다. ``EXACTLY``는 자식 뷰의 정확한 크기를 결정한다. ``AT_MOST``는 자식 뷰의 최대 범위를 지정한다. 자식 뷰는 범위 내에서 원하는 만큼 커질 수 있다. ``UNSPECIFIED``는 제약 조건이 없다는 뜻으로, 자식 뷰는 원하는 크기가 될 수 있다.<br/>