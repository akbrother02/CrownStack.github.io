---
title:  "IBInspectable and IBDesignable"
date:   2017-11-01
author: Pushpraj Chaudhary
categories:
- blog
tags:
- iOS
---


## IBInspectable
 ```@IBInspectable``` available from iOS 8.0. ```@IBInspectable``` properties provide the custom configuration and rendering of UIView and their subclasses. This is powerful mechanisms apply for XIB , NIB and StoryBoard.

Currently the following types support ``` @IBInspectable.```
* Int
*	CGFloat
*	Double
*	String
*	Bool
*	CGPoint
*	CGSize
*	CGRect
*	UIColor
*	UIImage


Steps with @IBInspectable property on a custom view:

** Step 1: **Create a class InspectableView parent of UIView. In which we set the variable of background color, corner radius, border width and border color with IBInspectable  .

```
class InspectableView: UIView {

    // Background Color.
    @IBInspectable var backgroundColor: UIColor? {
        didSet {
            backgroundColor = backColor
        }
    }

    // Corner Radius.
    @IBInspectable var cornerRadius: CGFloat = 0 {
        didSet {
            layer.cornerRadius = cornerRadius
            layer.masksToBounds = cornerRadius > 0
        }
    }

    // Border Width.
    @IBInspectable var borderWidth: CGFloat = 0 {
        didSet {
            layer.borderWidth = borderWidth
            layer.masksToBounds = borderWidth > 0
        }
    }

    // Border Color.
    @IBInspectable var borderColor : UIColor?{
        didSet{
            layer.borderColor = borderColor?.cgColor
        }
    }
}
```

## IBDesignable

@IBDesignable properties applied to the UIView and their subclasses and it render the view directly in StoryBoard, NIB and XIB, So that we can easily identify about the view before run the app.

Steps with @IBInspectable property on a custom view:

**Step 1 :** We already created a InspectableView class. By simply adding a prefix @IBDesignable to that class we got the functionality of IBDesignable in our custom UIView and in their subclasses. 

```
@IBDesignable
class InspectableView: UIView {

    // Background Color.
    @IBInspectable var backgroundColor: UIColor? {
        didSet {
            backgroundColor = backColor
        }
    }

    // Corner Radius.
    @IBInspectable var cornerRadius: CGFloat = 0 {
        didSet {
            layer.cornerRadius = cornerRadius
            layer.masksToBounds = cornerRadius > 0
        }
    }

    // Border Width.
    @IBInspectable var borderWidth: CGFloat = 0 {
        didSet {
            layer.borderWidth = borderWidth
            layer.masksToBounds = borderWidth > 0
        }
    }

    // Border Color.
    @IBInspectable var borderColor : UIColor?{
        didSet{
            layer.borderColor = borderColor?.cgColor
        }
    }
}
```
