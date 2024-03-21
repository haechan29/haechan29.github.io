---
title: View Lifecycle
layout: default
parent: Android
nav_order: 4
---

## 뷰는 어떻게 그려지나요?
### View가 그려지는 과정
1. Measure 단계
   - 목적: 각 뷰의 크기를 결정합니다.
   - 동작 방식: 레이아웃 매니저(LayoutManager)가 onMeasure 메서드를 호출하여 뷰가 자식 뷰를 포함하여 얼마나 많은 공간을 필요로 하는지 계산합니다. 이때, 부모 뷰로부터 받은 가용 공간(MeasureSpec)을 기반으로 계산이 이루어집니다. MeasureSpec은 크기와 모드(EXACTLY, AT_MOST, UNSPECIFIED)를 포함합니다. 
   - 결과: 각 뷰는 setMeasuredDimension(int width, int height) 메서드를 통해 자신의 크기를 결정합니다.
   <br/><br/>

2. Layout 단계
   - 목적: 뷰의 실제 위치를 부모 뷰 내에서 결정합니다.
   - 동작 방식: 레이아웃 매니저가 onLayout 메서드를 호출하여 자식 뷰에 실제 크기와 위치를 할당합니다. 이 단계에서는 measure 단계에서 결정된 크기를 바탕으로, 각 뷰의 위치를 상대적으로 결정합니다.
   - 결과: 각 뷰는 화면상에서의 정확한 위치와 크기를 갖게 됩니다.
   <br/><br/>

###  View의 생명 주기
1. 뷰 생성자: 뷰의 인스턴스를 생성.<br/>
2. onFinishInflate(): XML을 통해 뷰가 인플레이트된 후 호출.<br/>
3. onAttachedToWindow(): 뷰가 윈도우에 붙을 때 호출. 이 시점에서 뷰는 실제로 화면에 표시될 준비가 되었다고 볼 수 있으며, 이벤트 리스닝이나 애니메이션 시작과 같은 작업을 이 메서드 내에서 처리.<br/>
4. onMeasure(): 뷰의 크기를 결정하는 단계. 시스템에서 뷰에 얼마나 많은 공간을 할당할 수 있는지 알려주며, 뷰는 이 메서드를 통해 자신의 크기를 결정.<br/>
5. onLayout(): 뷰의 실제 크기와 위치를 결정.<br/>
6. onDraw(): Canvas, Paint 등의 객체를 사용하여 텍스트, 비트맵, 도형 등 뷰의 시각적 내용을 그린다.<br/>
<br/>

\+ invalidate(): 글자나 색상 등 크기 변화 없이 단순히 뷰의 속성 등이 변경되어 다시 그려야하는 경우 호출.<br/>
\+ requestLayout(): 뷰의 크기가 변화할 경우 레이아웃의 배치도 달라질 수 있기 때문에 해당 메소드를 호출함으로써 뷰들의 크기부터 다시 측정.<br/>

