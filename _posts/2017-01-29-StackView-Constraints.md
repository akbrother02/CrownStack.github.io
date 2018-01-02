---
title:  "Stack View and Programatically Constraints"
date:   2017-11-29
author: Satish Phogat
categories:
- blog
tags:
- iOS
---
#### 1) Stack View
 provides a streamlined interface for laying out a collection of views in either a column or a row.You can embed multiple UI objects into one by using stack views. For views embedded in a stack view, you no longer need to define auto layout constraints.
you select two or more view objects and then choose the Stack option. Interface Builder then embeds the objects into a stack view and resizes it automatically.
Furthermore, you can embed a stack view in another stack view to build more complex user interfaces
You still need to define the layout constrants for the stack view. It just saves you time from creating constraints for every UI element and makes it super easy to add/remove views from the layout.

<img src="/static/StackView.png" alt="Drawing" style="width: 600px;"/>

We take 3 stack views which contain UIViews .we embedded these stack view in single view .We arrange them in vertical axis and set its properties as shown screenshots.all enclosed stack view contain same property except middle one.That has Axis in horizontal direction.we have to set the constraints of only outermost stack view to super view which is shown in below image.

<img src="/static/StackViewConstraints.png" alt="Drawing" style="width: 600px;"/>

###### Distributions are of 5 types which are discussed below.
###### (i) Fill :
  The subviews are resized so as to fill the entire space available along the axis of the stack view. In other words the height of the subviews will be modified to fill the full height of the stack view in vertical orientation while the widths will be changed for a stack view in horizontal orientation. The amount by which each subview is resized relative to the other views can be controlled via the compression resistance and hugging priorities of the views.
###### (ii) FillEqually :
 The subviews are resized equally to fill the stack view along the view’s axis. In a vertical stack, therefore, all of the subviews will be of equal height whilst in a horizontal axis orientation the subviews will be of equal width.
###### (iii) FillProportionally :
 In this mode, the subviews are resized proportionally to their intrinsic content size along the axis of the stack view to fill the width or height of the view.
###### (iv) EqualSpacing :
Padding is used to space the subviews equally to fill the stack view along the axis. The size of the subviews will be reduced if necessary in order to fit within the available space based on the compression resistance priority setting and the position within the arrangedSubviews array.
###### (v) EqualCentering :
 This mode tries to position the subviews along the stack view’s axis such that the views have equal center to center spacing.

###### Alignment are also given of 5 types
###### (i) Fill:
 The width of the subviews in a vertical stack view are resized to fill the full width of the stack view.
###### (ii) Leading :
 In a vertically oriented stack view, the leading edges of the subviews are aligned with the leading edge of the stack view.
###### (iii) Trailing 
 In a vertically oriented stack view, the trailing edges of the subviews are aligned with the trailing edge of the stack view.
###### (iv) Center :
 The centers of the subviews are aligned with the center axis of the stack view.

#### 2) Programatically Set Constraints
You can also create constraints Programatically .Here i am to explain it using the NSLayoutConstraint class’s convenience method.
```
constraintWithItem:attribute:relatedBy:toItem:attribute:multiplier:constant:
```
Let’s discuss about the parameters of the NSLayoutConstraint(...) method.
###### The item 
is the graphic element that the constraint is applied to. In our case, it’s the myView view, but it could be anything else (button, label, image view, etc).
###### The attribute
describes in simple words the type of the constraint we set (like leading, trailing, top, and so on)
###### The relatedBy
 indicates the relation between the attribute property of the view that the constraint is applied to, and the attribute property of the other view that is related to, and it’s a NSLayoutRelation value.
###### The toItem 
is another view used as a “reference” for the constraint we create for our view.
###### The attribute 
parameter (second time) is the constraint type of the reference view (here the self.view) that is related to the attribute of the view that we create the constraint for.
###### The multiplier 
parameter multiplies the value of the second attribute parameter by the value given as an argument.
###### The constant 
value is actually added to the second attribute parameter value, so the first attribute parameter referring to the view set in the item produces the desired result.

We can set all constraints as described and add them with given item as follow

<img src="/static/Programatically Constraints.png" alt="Drawing" style="width: 600px;"/>
