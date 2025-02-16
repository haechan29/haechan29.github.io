---
title: 안드로이드의 렌더링 과정
layout: default
parent: Basic
grand_parent: Android
nav_order: 3.1
---

## 앱 화면은 어떻게 그려질까?
### 안드로이드의 렌더링 과정
1. 레이아웃 인플레이션.<br/>
   - 액티비티, 토스트, 다이어로그, 시스템바 등의 UI 요소는 각각 자신의 Window<sup>1</sup>를 가진다.<br/>
   - LayoutInflater를 통해 레이아웃을 Inflate<sup>3</sup>하고 Window에 부착한다.<br/><br/>

2. 크기, 위치 결정.<br/>
   - 뷰 트리를 순회하면서 각 뷰의 [onMeasure()] [1] 메서드를 호출하여 뷰의 크기를 결정한다.<br/>
   - 그 후, [onLayout()] [1] 메서드를 호출하여 각 뷰의 위치를 확정한다. 이 과정에서 뷰는 자신의 크기와 부모 및 자식 뷰와의 관계에 따라 자신의 위치를 계산한다.<br/><br/>

3. 드로잉.<br/>
   - 뷰의 크기와 위치가 결정되면, [onDraw()] [1] 메서드가 호출된다. Canvas 객체가 제공되며, 이를 통해 뷰를 그린다.<br/>
   - Canvas 외에도 복잡한 그래픽 처리를 위해 [OpenGL ES] [2], [Vulkan] [3] 등을 사용할 수 있다.<br/><br/>
   
4. 렌더링.<br/>
   - 캔버스에 그린 그림이 GPU에 의해 렌더링되어 Surface<sup>4</sup> 객체에 저장된다.<br/>
   - Window Manager가 모든 Window의 메타데이터를 SurfaceFlinger로 전송한다.<br/>
   - SurfaceFlinger는 각각의 Surface를 합성하여 최종 이미지를 생성한다.<br/><br/>

5. 화면 리프레시.<br/>
   - 화면의 리프레시율(Ex. 60Hz)에 맞춰 [VSYNC] [4] 신호가 발생하고 화면이 리프레시된다.<br/><br/>

<sup>1</sup>화면을 구성하는 단위. 하나의 Window는 하나의 레이아웃(뷰 객체 트리)와 매칭된다. WindowManager<sup>2</sup>을 통해 관리된다.<br/>
<sup>2</sup>Window의 생명 주기, 입력 및 포커스 이벤트, 화면 방향, 전환, 애니메이션, 위치, 변환, Z-order 등을 관리한다.<br/>
<sup>3</sup>레이아웃을 뷰 객체 트리로 변환하는 작업.<br/>
<sup>4</sup>화면에 그림을 그리기 위한 인터페이스. Window마다 하나씩만 존재하고, 내부적으로 이중 버퍼링<sup>5</sup>을 사용한다.<br/>
<sup>5</sup>화면에 표시되는 Front Buffer와 그림을 그리는 Back Buffer, 두 개의 그래픽 버퍼를 사용하는 방식. Back Buffer는 Lock 메커니즘을 통해 접근이 제어된다.<br/>

[1]: view%20lifecycle.html
[2]: https://source.android.com/docs/core/graphics/implement-opengl-es?hl=ko
[3]: https://source.android.com/docs/core/graphics/arch-vulkan?hl=ko
[4]: https://source.android.com/docs/core/graphics/implement-vsync?hl=ko