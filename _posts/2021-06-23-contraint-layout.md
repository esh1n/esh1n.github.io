---
title: "ConstraintLayout Review"
excerpt_separator: <!--more-->
header:
  overlay_image: https://developer.android.com/training/constraint-layout/images/constraint-fail_2x.png
  overlay_filter: 0.4
categories:
  - Development
  - Android
tags:
  - contraintlayout
  - ui
---

How to build complex UI in flat way.
<!--more-->


## Before beginning

![](https://sun9-14.userapi.com/impg/Cc2CQfgfqtFsnsPDOITg1EzJoKqc1hpBgiGOhw/pgypsJt2mk0.jpg?size=678x286&quality=96&sign=a9e0628adf30ac7a2bc20f97fced4b48&type=album)

Атрибут adjustViewBounds заставляет картинку подчиниться размеру компонента-контейнера. 

[android:adjustViewBounds](https://developer.android.com/reference/android/widget/ImageView#attr_android:adjustViewBounds): = Set this to true if you want the ImageView to adjust its bounds to preserve the aspect ratio of its drawable. 

## Basic Notes

- width ="0dp" Это match contraints. т.е указание constraint layout выстраивать ширину(или длину) исходя из указанных contstraints.

- how to set смещение , он же bias
  ![](https://github.com/esh1n/esh1n.github.io/blob/master/assets/images/2021-06-23-contraint-review/bias.png?raw=true)
  
- WRAP_CONTENT : enforcing constraints (Added in 1.1)

> If a dimension is set to WRAP_CONTENT, in versions before 1.1 they will be treated as a literal dimension -- meaning, constraints will not limit the resulting dimension. Чтобы при *wrap_content* уважал constraint то проставляй:

```xml 
	app:layout_constrainedWidth="true|false"
    app:layout_constrainedHeight="true|false"
```

- `app:layout_goneMarginTop="16dp"`

   > When a position constraint target’s visibility is View.GONE, you can also indicate a different margin value to be used.
   
### Работа с текстом

-baseline - когда текстовые вьюшки остаются на 1 мнимой линии

## Helpers

### Barrier
 
  Определяет где располагается конец опеределенной группы виджетов.
  ![](https://github.com/esh1n/esh1n.github.io/blob/master/assets/images/2021-06-23-contraint-review/barrier.png?raw=true)
  
  ![](https://github.com/esh1n/esh1n.github.io/blob/master/assets/images/2021-06-23-contraint-review/barrier2.png?raw=true)
  
### Flow
виртуальный помощник,позвол. описывать группу виджетов и задавать в ней правила по которым они размещаются.  
     ![](https://github.com/esh1n/esh1n.github.io/blob/master/assets/images/2021-06-23-contraint-review/flow.png?raw=true)
     
![](https://github.com/esh1n/esh1n.github.io/blob/master/assets/images/2021-06-23-contraint-review/flow_final.png?raw=true) 
> FLOW появился только в ConstraintLayout 2.0     
     
### Text Baseline
![](https://github.com/esh1n/esh1n.github.io/blob/master/assets/images/2021-06-23-contraint-review/text_baseline.png?raw=true)   

### Chain
> Это связка вьюшек друг за другом, имеющая отношения между собой.
Стиль chain:
- packed
- spread
- spread_inside  

### Guideline

