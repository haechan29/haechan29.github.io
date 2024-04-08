---
title: View Lifecycle
layout: default
parent: Basic
grand_parent: Android
nav_order: 4.1
---

## View의 생명주기는 어떻게 구성될까?
### View의 생명 주기
1. 뷰 생성자: 뷰의 인스턴스를 생성.<br/>
2. onFinishInflate(): XML을 통해 뷰가 인플레이트된 후 호출된다.<br/>
3. onAttachedToWindow(): 뷰가 윈도우에 붙을 때 호출된다.<br/>
4. onMeasure(): 뷰의 크기를 결정.<br/>
5. onLayout(): 뷰의 위치를 결정.<br/>
6. onDraw(): Canvas, Paint 등의 객체를 사용하여 텍스트, 비트맵, 도형 등을 그린다.<br/><br/>

\+ invalidate(): onDraw()부터 재시작한다. **뷰의 크기 변화 없이 글자나 색상 등의 속성이 변경되어 다시 그려야할때** 호출한다.<br/>
\+ requestLayout(): onMeasure()부터 재시작한다. **뷰의 크기가 변화하는 경우 호출**한다.<br/>

### View의 크기와 위치 결정하기
1. Measure 단계: 각 뷰의 실제적인 크기를 계산한다.<br/>
   - onMeasure() 메서드를 호출하여 뷰가 자식 뷰를 포함하여 얼마나 많은 공간을 필요로 하는지 계산한다.<br/>
   - 이때, 부모 뷰로부터 받은 가용 공간(MeasureSpec)<sup>1</sup>을 기반으로 계산이 이루어진다.<br/>
   - 각 뷰는 setMeasuredDimension(int width, int height) 메서드를 통해 자신의 크기를 결정한다.<br/><br/>

2. Layout 단계: 각 뷰의 실제 위치를 결정한다.<br/>
   - onLayout() 메서드를 호출하여 자식 뷰에 실제 위치를 할당한다.<br/>
   - Measure 단계에서 결정된 크기를 바탕으로, 각 뷰의 위치를 상대적으로 결정한다.<br/><br/>

<sup>1</sup>자식 뷰의 너비 또는 높이에 대한 요구 사항. 크기와 모드로 구성되며, 세 가지 모드가 있다. EXACTLY는 자식 뷰의 정확한 크기를 결정한다. AT_MOST는 자식 뷰의 최대 범위를 지정한다. 자식 뷰는 범위 내에서 원하는 만큼 커질 수 있다. UNSPECIFIED는 제약 조건이 없다는 뜻으로, 자식 뷰는 원하는 크기가 될 수 있다.<br/>