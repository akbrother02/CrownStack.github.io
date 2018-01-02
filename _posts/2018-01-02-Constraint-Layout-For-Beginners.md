#### **What is ConstraintLayout?**

ConstraintLayout is a powerful new class, it is basically an enhanced version of RelativeLayout but helps us to manage the things in more easier way and in effective manner. It helps us to lay the child view using “constraints” relative to each other in a position based relationship.

It helps to improve the performance of our layout because it reduces the nesting of views. Unlike Relative Layout, here we have “anchors” which provides more control over the view positioning.

#### **Constraint Handles:**

‘Constraint‘ is a defined rule for view which set the positioning and alignment of it on the screen. There are several constraints that a constraint class support here are these handles:

*Resizing:*
Resize handle provides an anchor which resizes the layout in the layout editor. Resizing a view using the resize anchor in the layout editor will automatically recalculate the constraints that have been previously set on that view.


<img src="/static/ConstraintLayout-1f1d079c.png" alt="Drawing" style="width: 250px;"/>    <img src="/static/ConstraintLayout-0ffe9c98.png" alt="Drawing" style="width: 320px;"/>


*Side Constraint:*
These constraints allow to position the view within the layout. For instance, for any selected view it will help to position it in the left or the right. This is done in the layout editor by dragging the anchor point of one view with the other view’s anchor point.

<img src="/static/ConstraintLayout-0ffe9c98.png" alt="Drawing" style="width: 320px;"/>

*Vertical Bias:*
Vertical Bias allows a view to be align on vertical axis. This Bias will be relative to its constraint position.

<img src="/static/ConstraintLayout-a8902b47.png" alt="Drawing" style="width: 420px;"/>


*Horizontal Bias:*
Vertical Bias allows a view to be align on horizontal axis. This Bias will be relative to its constraint position.

<img src="/static/ConstraintLayout-f4fe197c.png" alt="Drawing" style="width: 420px;"/>


*Baseline Constraint:*
Baseline Constraint allows to align baseline of one textview with another or multiple other textviews, irrespective of their text size. One important thing here is that baseline constraints of one view can only be aligned with baseline constraint of another textview.

This can be done by aligning the baseline of one view with another in the layout editor.

<img src="/static/ConstraintLayout-179e157e.png" alt="Drawing" style="width: 420px;"/>

<img src="/static/ConstraintLayout-cee83873.png" alt="Drawing" style="width: 420px;"/>


**Setting size of a view**

There are three type of size in the ConstraintLayout that you can set for a view. These sizes will allow that view’s size in accordance with its relative layouts with constraints. These three view sizes are:

 - Match Parent
 - Wrap Content
 - Fixed Size

**a.** Those `zigzag` lines in the layout editor below represent that this layout is “Match Parent”  you can click it to change it.

<img src="/static/ConstraintLayout-89f42c6b.png" alt="Drawing" style="width: 420px;"/>


**b.** Those `>>> <<<` in the below layout editor represents that this view is set to “Wrap Content” which means it will take as much size on the screen as it requires and will adjust according the content available. You can get this option by just clicking these lines to change or to get it.

<img src="/static/ConstraintLayout-21e4afd1.png" alt="Drawing" style="width: 420px;"/>


**c.** It represents that the  height and width of the view is fixed in size which is measure in dp. It looks like a pipe `I` symbol in the layout editor,

<img src="/static/ConstraintLayout-7ccce4b1.png" alt="Drawing" style="width: 420px;"/>


**Deleting Constraints**
We can delete the constraint that sometime is required to position it more accurately. It is very useful feature and is often used to design and position views in the layout.  Here you can see how to delete single constraint at a time.

<img src="/static/ConstraintLayout-6c78f925.png" alt="Drawing" style="width: 420px;"/>

In case if you want to delete all the constraint in one go you can do that as well like the below image.

<img src="/static/ConstraintLayout-5a62264c.png" alt="Drawing" style="width: 420px;"/>


ConstraintLayout is very easy to learn and provide great flexibility while designing various screens for an app. Above described tools are the only tools that you may need to use, for having ConstrainLayout for designing. Here you can position all the views right from the Layout Editor itself.

That's all for ConstraintLayout!!

Please don't hesitate to bother if you need any help.
