---
title:  "IBInspectable and IBDesignable"
date:   2017-11-01
author: Pushpraj Chaudhary
categories:
- blog
tags:
- iOS
---


In Xcode 6 and iOS8 two new interface builder declaration attributes were introduced to design, build and integrate custom controls directly in the Interface Builder: `IBInspectable` and `IBDesignable`.

## IBInspectable

```@IBInspectable``` provide the custom configuration and rendering of UIView and their subclasses at runtime. This is powerful mechanism apply for XIB and StoryBoard.

The most useful use case for IBInspectable, is being able to change the cornerRadius, borderWidth and borderColor of a UIView and their subclasses from attribute inspector, something that most probably every iOS developer has to deal with during the development of an App.

Currently the following types support ` @IBInspectable.`
*   Int
*	CGFloat
*	Double
*	String
*	Bool
*	CGPoint
*	CGSize
*	CGRect
*	UIColor
*	UIImage

Those who are already familiar with runtime attributes will have noticed in above list of types. UIColor is the only color type supported, not the CGColor.


**Step 1:** Create a subclass CSDesignableView for UIView. In which we set the variable of corner radius, border width and border color with IBInspectable.

```swift
class CSDesignableView: UIView {
    
    @IBInspectable var borderColor : UIColor = UIColor.clear{
        didSet{
            self.layer.borderColor = self.borderColor.cgColor
        }
    }
    
    @IBInspectable var borderWidth : CGFloat = 0{
        didSet{
            self.layer.borderWidth = self.borderWidth
        }
    }
    
    @IBInspectable var cornerRadius : CGFloat = 0{
        didSet{
            self.layer.cornerRadius = self.cornerRadius
        }
    }
}

class CSDesignableButton: UIButton {
    
    @IBInspectable var borderColor : UIColor = UIColor.clear{
        didSet{
            self.layer.borderColor = self.borderColor.cgColor
        }
    }
    
    @IBInspectable var borderWidth : CGFloat = 0{
        didSet{
            self.layer.borderWidth = self.borderWidth
        }
    }
    
    @IBInspectable var cornerRadius : CGFloat = 0{
        didSet{
            self.layer.cornerRadius = self.cornerRadius
        }
    }
}

class CSDesignableTextField: UITextField {
    
    @IBInspectable var borderColor : UIColor = UIColor.clear{
        didSet{
            self.layer.borderColor = self.borderColor.cgColor
        }
    }
    
    @IBInspectable var borderWidth : CGFloat = 0{
        didSet{
            self.layer.borderWidth = self.borderWidth
        }
    }
    
    @IBInspectable var cornerRadius : CGFloat = 0{
        didSet{
            self.layer.cornerRadius = self.cornerRadius
        }
    }
    
    @IBInspectable var placeHolderColor: UIColor? {
        get
        {
            return self.placeHolderColor
        }
        set {
            self.attributedPlaceholder = NSAttributedString(string:self.placeholder != nil ? self.placeholder! : "", attributes:[NSForegroundColorAttributeName: newValue!])
        }
    }
}

class CSDesignableLabel: UILabel {
    
    @IBInspectable var borderColor : UIColor = UIColor.clear{
        didSet{
            self.layer.borderColor = self.borderColor.cgColor
        }
    }
    
    @IBInspectable var borderWidth : CGFloat = 0{
        didSet{
            self.layer.borderWidth = self.borderWidth
        }
    }
    
    @IBInspectable var cornerRadius : CGFloat = 0{
        didSet{
            self.layer.cornerRadius = self.cornerRadius
        }
    }
}

class CSDesignableImageView: UIImageView {
    
    @IBInspectable var borderColor : UIColor = UIColor.clear{
        didSet{
            self.layer.borderColor = self.borderColor.cgColor
        }
    }
    
    @IBInspectable var borderWidth : CGFloat = 0{
        didSet{
            self.layer.borderWidth = self.borderWidth
        }
    }
    
    @IBInspectable var cornerRadius : CGFloat = 0{
        didSet{
            self.layer.cornerRadius = self.cornerRadius
        }
    }
}
```

**Step 2 :**  In the Interface Builder (`StoryBoard`) drag and drop a UI component. Go to the `Show the Identity Inspector` and set the Class for that UI component.

<img src="/static/IBInspectable_SetClass.png" alt="Drawing" style="width: 600px;"/>

**Step 3 :**  When we set the subclass then its defined properties are display in the Attributes Inspector. In below image we can see how user can easily use those properties according to their project's need. 

<img src="/static/IBInspectable_UseOfProperties.png" alt="Drawing" style="width: 600px;"/>


**Step 4 :**  After applying needed properties, Run your app and we can see our work in simulator like below one.

<img src="/static/IBInspectable_Simulator.png" alt="Drawing" style="width: 600px;"/>


## IBDesignable

One of the more powerful features introduced to design, build and integrate custom controls directly in the Interface Builder. Previously, we were able to subclass UIView or any of the UIKit control classes, but we couldn’t really see the results of our customizations until runtime. Now, we are able to see our custom controls in Interface Builder(storyBoard, nib and xib) exactly as they are going to be rendered live, and this really helps a lot when implementing a concrete design for an App.


**Step 1 :** We already created a CSDesignable class for various UI componenets. By simply adding a prefix @IBDesignable to that class we got the functionality of IBDesignable in ui components. 

```swift
@IBDesignable
class CSDesignableView: UIView {
    
    @IBInspectable var borderColor : UIColor = UIColor.clear{
        didSet{
            self.layer.borderColor = self.borderColor.cgColor
        }
    }
    
    @IBInspectable var borderWidth : CGFloat = 0{
        didSet{
            self.layer.borderWidth = self.borderWidth
        }
    }
    
    @IBInspectable var cornerRadius : CGFloat = 0{
        didSet{
            self.layer.cornerRadius = self.cornerRadius
        }
    }
}

@IBDesignable
class CSDesignableButton: UIButton {
    
    @IBInspectable var borderColor : UIColor = UIColor.clear{
        didSet{
            self.layer.borderColor = self.borderColor.cgColor
        }
    }
    
    @IBInspectable var borderWidth : CGFloat = 0{
        didSet{
            self.layer.borderWidth = self.borderWidth
        }
    }
    
    @IBInspectable var cornerRadius : CGFloat = 0{
        didSet{
            self.layer.cornerRadius = self.cornerRadius
        }
    }
}

@IBDesignable
class CSDesignableTextField: UITextField {
    
    @IBInspectable var borderColor : UIColor = UIColor.clear{
        didSet{
            self.layer.borderColor = self.borderColor.cgColor
        }
    }
    
    @IBInspectable var borderWidth : CGFloat = 0{
        didSet{
            self.layer.borderWidth = self.borderWidth
        }
    }
    
    @IBInspectable var cornerRadius : CGFloat = 0{
        didSet{
            self.layer.cornerRadius = self.cornerRadius
        }
    }
    
    @IBInspectable var placeHolderColor: UIColor? {
        get
        {
            return self.placeHolderColor
        }
        set {
            self.attributedPlaceholder = NSAttributedString(string:self.placeholder != nil ? self.placeholder! : "", attributes:[NSForegroundColorAttributeName: newValue!])
        }
    }
}

@IBDesignable
class CSDesignableLabel: UILabel {
    
    @IBInspectable var borderColor : UIColor = UIColor.clear{
        didSet{
            self.layer.borderColor = self.borderColor.cgColor
        }
    }
    
    @IBInspectable var borderWidth : CGFloat = 0{
        didSet{
            self.layer.borderWidth = self.borderWidth
        }
    }
    
    @IBInspectable var cornerRadius : CGFloat = 0{
        didSet{
            self.layer.cornerRadius = self.cornerRadius
        }
    }
}

@IBDesignable
class CSDesignableImageView: UIImageView {
    
    @IBInspectable var borderColor : UIColor = UIColor.clear{
        didSet{
            self.layer.borderColor = self.borderColor.cgColor
        }
    }
    
    @IBInspectable var borderWidth : CGFloat = 0{
        didSet{
            self.layer.borderWidth = self.borderWidth
        }
    }
    
    @IBInspectable var cornerRadius : CGFloat = 0{
        didSet{
            self.layer.cornerRadius = self.cornerRadius
        }
    }
}
```

**Step 2 :**  In the Interface Builder (`StoryBoard`) drag and drop a UI component. Go to the `Show the Identity Inspector` and set the Class for that UI component. 

***Note:***  Sometime designables keep on update for long time, till then you will not be able see live rendering of UI components, as u can see in beloww screenshot that designables are up to date. Solution is provided in the end of the blog.

<img src="/static/IBDesignable_SetClass.png" alt="Drawing" style="width: 600px;"/>


**Step 3 :**  When subclass is set its defined properties are display in the Attributes Inspector, use properties according to your project's need. In below image you can see how user can easily use those properties. 

<img src="/static/IBDesignable_UseOfProperties.png" alt="Drawing" style="width: 600px;"/>


<img src="/static/IBDesignable_UseOfProperties2.png" alt="Drawing" style="width: 600px;"/>



**Important:** Sometime Xcode causes problems when displaying the designable controls in IB. When this problem arise  If you find that your designable controls are working in the simulator or in a device, but won’t display in IB, try these steps:

* While in a storyboard, go to “Editor” in the top bar menu
* uncheck “Automatically refresh views” if it is.
* clean your project.
* Go to “Editor” again and click “Refresh All Views”
