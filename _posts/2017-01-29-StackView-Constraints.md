---
title:  "Stack View and Programatically Constraints"
date:   2017-11-29
author: Satish Phogat
categories:
- blog
tags:
- iOS
---
### 1) Stack View

 We can embed multiple UI objects into one by using stack views. For views embedded in a stack view, you no longer need to define auto layout constraints.
We select two or more view objects and then choose the Stack option. Interface Builder then embeds the objects into a stack view and resizes it automatically.
We can embed a stack view in another stack view to build more complex user interfaces

<img src="/static/StackView1.png" alt="Drawing" style="width: 700px;"/>

We have taken 3 stack views which contain UIViews .First StackView contains 2 views with orange background and second StackView constains 2 view with blue background and last StackView has 3 views with green background. We embedded these stack views in single StackView. We arrange all 3 stack views in vertical axis and set its properties as shown screenshots.all enclosed stack view contain same property except middle one.As views of middle stack are arranged in horizontal direction.We have to set the constraints of only outermost stack view to super view which is shown in below image.

<img src="/static/StackViewConstraints.png" alt="Drawing" style="width: 600px;"/>

StackView contains 4 properties : Axis, Distributions, Alignment and spacing.

###### Axis
This is of 2 types.

###### i) Vertical Axis -
This will arrange the subviews in vertical direction.

###### ii) Horizontal Axis -
This will arrange the subviews in horizontal direction.

###### Alignment are also given of 5 types

###### (i) Fill:
 The width of the subviews in a vertical stack view are resized to fill the full width of the stack view. In 1st screenshot we have taken fill Alignment.

###### (ii) Leading :
 In a vertically oriented stack view, the leading edges of the subviews are aligned with the leading edge of the stack view.

###### (iii) Trailing 
 In a vertically oriented stack view, the trailing edges of the subviews are aligned with the trailing edge of the stack view.

###### (iv) Center :
 The centers of the subviews are aligned with the center axis of the stack view.

###### Distributions are of 5 types which are discussed below.
###### (i) Fill :
  In this type, one of view will increase its size to occupy the increased space while second will remain same.
###### (ii) FillEqually :
 This type will will increase the size of all view equally and occupy the increased size of stack view. In our screenshot we are showing the subviews in FillEqually mode as all the subviews are having same height.
###### (iii) FillProportionally :
 This mode will increase or decrease size of view according to their respective proportion.Suppose one view has height 200, second 100 and StackView has increase with 30 then first view will occupy height 220 and second view 110.
###### (iv) EqualSpacing :
This type adjusts the spacing between subviews without resizing the subviews themselves.
###### (v) EqualCentering :
 attempts to ensure the centers of each subview are equally spaced.

###### spacing :
It will define the spacing between stack views and its subviews.We have taken 10 spacing between StackViews and same spacing between subviews of different StackView.

***
