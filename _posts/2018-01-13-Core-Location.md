---
title:  "Geofencing"
date:   2018-01-13
author: Satish Phogat
categories:
- blog
tags:
- iOS
---
###  Geofencing

Core Location Framework provides services for determining a user's geographic location.

We have to create region called Geofences region. Geofences in iOS are regions with a latitude and longitude. Notifications are sent when a user's device enters or exits that defined region.

Lets starts with new Project. Drag & drop mkMapView in storyboard and add its constraints attached to Super View border. Create its outlet in ViewController and attach its delegate.

Apple wants to keep its user's location secret so if we want to access their location we have to take permission from them. We will write below code to info.plist source code.

```
<key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
	<string></string>
	<key>NSLocationAlwaysUsageDescription</key>
	<string>true</string>
	<key>NSLocationWhenInUseUsageDescription</key>
	<string></string>
	<key>UIBackgroundModes</key>
	<array>
		<string>location</string>
	</array>
  ```

When app will launch , this will show a pop up to user to allow the access his location. If user click on allow button then it will give access.

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

```
override func viewDidAppear(_ animated: Bool) {
     super.viewDidAppear(animated)

     if CLLocationManager.authorizationStatus() == .notDetermined {
         locationManager.requestAlwaysAuthorization()
     } else if CLLocationManager.authorizationStatus() == .denied {
         // Show alert to user to enable access location service from app setting
     } else {
         locationManager.startUpdatingLocation()
     }
 }
 ```
As explained in above image, If authorization status is not determined then it should allow always and when it is denied then it should send an alert to user for enable it from app setting of device. If it didn't meet any of 2 condition then it should start updating location.

Delegates of mkMapView and locationManager are requied to set.Call these methods in viewDidLoad method as given below.

```
func setUpMapView() {
    // For mkMapView
    mkMapView.delegate = self
    mkMapView.showsUserLocation = true

    //For location manager
    locationManager.delegate = self
    locationManager.distanceFilter = 100
    locationManager.desiredAccuracy = kCLLocationAccuracyBest
}
```
We need to create the circular Geofence regions where we will check user entry or exit. Coordinate of latitude and longitude will be required. Center can be find out from these coordinates using below statement.
```
CLLocationCoordinate2DMake(latitude, longitude)
```
We can create cirles by passing these center and radius to MKCircle method. Finally these circle will be added to mkMapView as shown in below screenshot.Here we are taking multiple coordinates.

```
func setUpGeofenceRegion() {

    let geofenceLocationCenterArray = [CLLocationCoordinate2DMake(28.486645, 77.105037),CLLocationCoordinate2DMake(30.486645, 86.105037),CLLocationCoordinate2DMake(31.486645, 86.105037),CLLocationCoordinate2DMake(35.486645, 86.105037)]

    for center in geofenceLocationCenterArray {
        let circularRegion = MKCircle(center: center, radius: 50000)
        mkMapView.add(circularRegion)
    }
}
```
One delegate method is required to set up to define layout of circular region as we want. See the below screenshot.

```
func mapView(_ mapView: MKMapView, rendererFor overlay: MKOverlay) -> MKOverlayRenderer {
     let circleRenderer = MKCircleRenderer(overlay: overlay)
     circleRenderer.strokeColor = .red
     circleRenderer.lineWidth = 2.0

     return circleRenderer
 }
```
One thing we need to keep in mind that geofence will work when authorization status is .authorizedAlways. We will set this to notify when user enter or exit the defined region as per requirment. Use below delegate method to do the same.

```
extension ViewController: CLLocationManagerDelegate {

    func locationManager(_ manager: CLLocationManager, didEnterRegion region: CLRegion) {
        print("entered in region" + String(describing: manager.location?.coordinate))
    }

    func locationManager(_ manager: CLLocationManager, didExitRegion region: CLRegion) {
        print("exit from specified region")
    }

    func locationManager(_ manager: CLLocationManager, didChangeAuthorization status: CLAuthorizationStatus) {
        if (status == .authorizedAlways) {
            setUpGeofenceRegion()
        }
    }
}
```
Write the whole code in single ViewController and execute. We will see user location and regions on map and required functionality. Modify it as you wish.

**Note** : We can update user's location from storyboard also to test as shown in below screenshot.

<img src="/static/LocationUpdate.png" alt="Drawing" style="width: 600px;"/>


Thanks :)
