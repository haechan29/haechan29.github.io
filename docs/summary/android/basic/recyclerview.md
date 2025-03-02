---
title: RecyclerView
layout: default
parent: Basic
grand_parent: Android
date: 2025-03-02
nav_order: 15
---

## RecyclerView에 아이템이 어떻게 추가될까?
RecyclerView는 아이템이 변경되었는지, ViewHolder을 재활용할 수 있는지를 확인하여 효율적으로 UI를 그린다.<br/>

### 변경된 아이템 파악하기<sup>1</sup>
변경된 아이템은 크게 4가지 방법으로 처리된다.<br/>

1. 모든 뷰 새로 그리기<br/>
   - `Adapter#notifyDataSetChanged`를 호출하는 경우에 해당한다.<br/>
   - 가장 단순하지만 비용이 많이 들기 때문에 사용하지 않는 것이 좋다.<br/>
2. 특정 뷰 추가/삭제하기<br/>
   - `Adapter#nofityItemInserted`/ `Adapter#nofityItemRemoved`를 호출하는 경우에 해당한다.<br/>
   - 기존 아이템이나 새로운 아이템이 동일한 item<sup>2</sup>을 찾지 못한 경우에 해당한다.<br/>
   - 특정 뷰를 다시 그리고, 그 뒤의 뷰의 위치를 옮긴다.<br/>
3. 특정 뷰 위치 바꾸기<br/>
   - `Adapter#nofityItemMoved`를 호출하는 경우에 해당한다.<br/>
   - 기존 아이템과 새로운 아이템의 item과 content<sup>3</sup>가 모두 동일하지만 position이 다른 경우에 해당한다.<br/>
   - 뷰는 다시 그리지 않고, 두 뷰의 위치를 옮긴다.<br/>
4. 특정 뷰 새로 그리기<br/>
   - `Adapter#nofityItemChanged`를 호출하는 경우에 해당한다.<br/>
   - 기존 아이템과 새로운 아이템의 item이 동일하지만 content가 다른 경우에 해당한다.<br/>
   - 특정 뷰만 다시 그린다<sup>4</sup>.<br/>

### ViewHolder 재활용하기
아이템을 부착할 뷰홀더가 있는지 확인한다. 있다면 해당 뷰홀더를 사용하고, 없다면 새로 만든다.<br/>
뷰홀더는 아래 순서로 생성 및 재활용된다.<br/>

1. `submitList` 호출시 ViewType을 기반으로 캐시<sup>5</sup> 확인.<br/>
2. `onCreateViewHolder`: (캐시된 뷰홀더가 없는 경우) 뷰홀더 생성.<br/>
3. `onBindViewHolder`: 아이템을 뷰홀더에 바인딩.<br/>
4. `onAttachedToWindow`: 뷰가 화면에 보이게 되었을 때 호출.<br/>
5. `onDetachedToWindow`: 뷰가 화면에 보이지 않게 되었을 때 호출.<br/>
6. `onViewRecycled`: 뷰홀더가 다시 사용될 수 있도록 바인딩된 아이템 제거. 이후 `onBindViewHolder` 재호출.<br/>


<sup>1</sup>`Adapter#setHasStableIds`를 사용하지 않을 때 기준. 이를 사용하면 `Adapter#getItemId`의 반환값을 기준으로 변경 여부를 확인한다.<br/> 
<sup>2</sup>`DiffUtil.ItemCallback#areItemsTheSame` 메서드가 비교하는 값.<br/>
<sup>3</sup>`DiffUtil.ItemCallback#areContentsTheSame` 메서드가 비교하는 값.<br/>
<sup>4</sup>`RecyclerView#setHasFixedSize`를 사용하면 뷰를 다시 그리는 과정을 최적화할 수 있다.<br/>
<sup>5</sup>LayoutManager 캐시, RecyclerView 캐시, 전역 RecyclerViewPool.<br/>
