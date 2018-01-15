---
title:  "Core Location Tutorial"
date:   2018-01-13
author: Satish Phogat
categories:
- blog
tags:
- iOS
---
###  Core Location

Core Location Framework provides services for determining a user's geographic location.

We have to create region called Geofences region.Geofences in iOS are regions with a latitude and longitude. Notifications are sent when a user's device enters or exits that defined region.

Lets starts with new Project. Drag & drop mkMapView in storyboard and add its constraints attatched to Super View border.Create its outlet in ViewController and attach its delegate.

Apple wants to keep its user's location secret so if we want to access their location we have to take permission from them. We will write below code to info.plist source code.

<img src="/static/InfoPist.png" alt="" style="width: 700px;"/>

When app will launch , this will show a pop up to allow to access user location.If user click on allow button then it will give access.

First of all, we have to import Framework class in ViewController.

```
import MapKit
import CoreLocation
```

and inherit the ViewController with CLLocationManagerDelegate and making instance of CLLocationManager class as below.

```
let locationManager = CLLocationManager()
```

When view appears on screen , we have to check the user authorization status by using below line of code.

<img src="/static/AuthorizationStatus.png" alt="Drawing" style="width: 600px;"/>

As explained in above image, If authorization status is not determined then it should allow always and when it is denied then it should send an alert to user for enable it from app setting of device. If it didn't meet any of 2 condition then it should start updating location.

Delegates of mkMapView and locationManager are requied to set.Call these methods in viewDidLoad method as given below.

<img src="/static/DelegateMethod.png" alt="Drawing" style="width: 600px;"/>

We need to create the circular Geofence regions where we will check user entry or exit. Coordinate of latitude and longitude will be required. Center can be find out from these coordinates using below statement.
```
CLLocationCoordinate2DMake(latitude, longitude)
```
We can create cirle by passing these center and radius to MKCircle method. Finally these circle will be added to mkMapView as shown in below screenshot.Here we are taking multiple coordinates.

<img src="/static/GeofenceRegion.png" alt="Drawing" style="width: 600px;"/>

One delegate method is required to set up to define layout of circular region as we want. See the below screenshot.

<img src="/static/RenderOverlayImage.png" alt="Drawing" style="width: 600px;"/>

One thing we need to keep in mind that geofence will work when authorization status is .authorizedAlways. We will set this to notify when user enter or exit the defined region as per requirment. Use below delegate method to do the same.

<img src="/static/LocationDelegateMethod.png" alt="Drawing" style="width: 600px;"/>

Write the whole code in single ViewController and execute. We will see user location and regions on map and required functionality. Modify it as you wish.

Thanks :)
