---
title: ConstraintLayout
layout: default
parent: Etc
nav_order: 9
---

## ConstraintLayout
### ConstraintLayout의 장점
- 플랫 레이아웃 구조: ConstraintLayout을 사용하면 복잡한 계층 구조 없이도 복잡한 레이아웃을 만들 수 있습니다. 이는 <a src="https://haechan29.github.io/docs/etc/view%20lifecycle.html">렌더링 시간을 단축시키고 애플리케이션의 성능을 향상시킵니다.</a> 중첩된 레이아웃 대신 한 레벨의 레이아웃으로 구성이 가능합니다.
- 멀티스크린 지원: ConstraintLayout은 다양한 화면 크기, 해상도 및 밀도를 지원합니다. 이는 개발자가 단일 레이아웃을 사용하여 여러 기기에서 일관된 UI를 제공할 수 있게 해줍니다.

+ View가 그려지는 과정
  1 .Measure 단계
- 목적: 각 뷰의 크기를 결정합니다.
- 동작 방식: 레이아웃 매니저(LayoutManager)가 onMeasure 메서드를 호출하여 뷰가 자식 뷰를 포함하여 얼마나 많은 공간을 필요로 하는지 계산합니다. 이때, 부모 뷰로부터 받은 가용 공간(MeasureSpec)을 기반으로 계산이 이루어집니다. MeasureSpec은 크기와 모드(EXACTLY, AT_MOST, UNSPECIFIED)를 포함합니다.
- 결과: 각 뷰는 setMeasuredDimension(int width, int height) 메서드를 통해 자신의 크기를 결정합니다.

2. Layout 단계
- 목적: 뷰의 실제 위치를 부모 뷰 내에서 결정합니다.
- 동작 방식: 레이아웃 매니저가 onLayout 메서드를 호출하여 자식 뷰에 실제 크기와 위치를 할당합니다. 이 단계에서는 measure 단계에서 결정된 크기를 바탕으로, 각 뷰의 위치를 상대적으로 결정합니다.
- 결과: 각 뷰는 화면상에서의 정확한 위치와 크기를 갖게 됩니다.

