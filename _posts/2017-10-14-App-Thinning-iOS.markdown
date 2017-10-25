---
title:  "App Thinning iOS"
date:   2017-10-14
author: Pushpraj Chaudhary
categories:
- blog
tags:
- iOS
---

App Thinning was introduced with Xcode 7 (iOS 9), with the main emphasis on tailoring the App delivery to the capabilities of the user’s particular device, with minimal footprint which in turn leads to decrease in the app size.

Apps are downloaded more quickly and have less impact on the limited storage on the device and cellular data limits, this will pretty much be automatically handled via the App Store and requires little or no effort on the development side.

Let’s take a closer look at what this feature is, and how it can help both developers and the users they are targeting.
iOS 9 enables mobile app developers to decrease the size of their app on users’ mobile devices through app thinning. This involves using one or a combination of three processes.

**Slicing:** Use an Asset Catalog to install assets on specific devices.
**Bitcode:** Submit partially compiled code that will be optimized by the App Store.
**On-demand resources:** Specific assets are stored in the App Store and downloaded by the application when they are needed, and purged by iOS when disk space is low.

The optimizations help reduce the size of the application when the user installs it and reduces the application's memory footprint.

*bitcode* is the most relevant for non-gaming related apps.
*On-demand resources* is the most relevant for gaming related apps.



## Slicing

Slicing is the process of creating different variations of app bundle for different target devices. A variant contains only the executable architecture and resources those are needed for the target device. The store will create and deliver different variants based on the devices your app supports. Image resources are sliced according to their resolution and device family. GPU resources are sliced according to device capabilities. For tvOS apps, assets in catalogs shared between iOS and tvOS targets are sliced and large app icons are removed. When the user installs an app, a variant for the user’s device is downloaded and installed.

Images stored in 1x, 2x, and 3x format will automatically be sliced per device according to the device’s native resolution. So, your resources must be organized in asset catalogs. Secondly, you should also make sure you have all available architectures (arm64 armv7 armv7s) enabled in your “Build Settings” under “Valid Architectures”.

<img src="/static/app_thinning_slicing.png" alt="Drawing" style="width: 600px;"/>



## On-Demand Resources

On Demand Resources is another great way to minimize your app size. It enable faster downloads and smaller app sizes, improving the first-time launch experience. This is useful for very large apps, especially ones that you would like to stay within the cellular data download limit. For example, a game app may divide resources into game levels and request the next level of resources only when the app anticipates that the user will move to that level. Similarly, the app can request In-App Purchase resources only when the user buys the corresponding in-app purchase.

For users, on-demand resources work transparently in the background, supplying resources as needed while the user explores the features of your app.

Enabling on demand resources involves changing the “Enable On Demand Resources” boolean to “Yes” in Xcode settings (under Build
   Settings).

<img src="/static/app_thinning_on_demand.png" alt="Drawing" style="width: 600px;"/>

There are three main categories On Demand Resources..

1. Initial Install Tags
   * These are resources required for the app to run.
   * They will be automatically downloaded during the initial app download.
2. Prefetch Tags
   * These will be downloaded during the first run of the app after the app has already been installed.
3. Download Only On Demand Resources
   * These will be downloaded only when requested by the app, where the tags you add can be fetched with an    NSBundleResourceRequest.

   The list of the size limits is this;

* An iOS App Bundle cannot be larger than 2GB.
* A tvOS App Bundle cannot be larger than 200MB.
* A tag cannot contain resources larger than 512MB, while the total size of Initial Install Tags cannot exceed 2GB.
* Similarly, Initial Installed Tags and Prefetched Tags cannot exceed a total size of 2GB.
* When using a NSBundleResourceRequest to fetch/use tags, the total size of the tags currently in use cannot be larger than 2GB.
* Lastly, the total size of On-Demand Resources hosted on the App Store cannot be larger than 20GB.

Implementing On-Demand Resource management in app
Initializing a Resource Request

init(tags:) and init(tag:bundle:) are used to Initialize a resource request for managing the on-demand resources marked with any of the set of specified tags. The managed resources are loaded into the main bundle or specific bundle respectively.

Basically, three methods are used to access the resources.

### func beginAccessingResourcesWithCompletionHandler(_:)
This method requests access to the resources marked with the managed tags. If any of the resources are not on the device, they are requested from the App Store.

### func conditionallyBeginAccessingResourcesWithCompletionHandler(_:)
This method first checks availability on the device then requests access to the resources marked with the managed tags. If any of the resources are not on the device, they are requested from the App Store.

### func endAccessingResources()
This method informs the system that you have finished accessing the resources marked with the tags managed by the request.

This code snippet shows how to implement the method in swift.
```swift
let tags = NSSet(array: [“tag1″,”tag2″])
let resourceRequest = NSBundleResourceRequest(tags: tags as! Set<String>)
resourceRequest.conditionallyBeginAccessingResourcesWithCompletionHandler {(resourcesAvailable: Bool) -> Void in
   if resourcesAvailable {
       // Do something with the resources
   } else {
       resourceRequest.beginAccessingResourcesWithCompletionHandler {(err: NSError?) -> Void in
           if let error = err {
               print(“Error: \(error)”)
           } else {
               // Do something with the resources
           }
       }
   }
}
```


## Bitcode

The final process in app thinning is bitcode, if your app is uploaded to the store in bitcode, future updates and optimizations can be made automatically by the App Store itself, adding to any potential improvements that developers make to their apps.

However, the introduction of bitcode means developers will no longer upload a singular binary file, but an intermediate representation of a compiled program. This will be compiled on demand when installed by the user. Compilation occurs by Apple identifying the device it is being installed onto, picking the assets required for that particular device, and compiling them into a file ready for the user to install.

This feature works along with the rest of the two processes to ensure that the size of the app is kept to the minimum.

One of the biggest advantages of this process is ensuring that 8GB and 16GB iPhones and iPads remain relevant, which is particularly important as developers and brands target emerging markets

This can be enable in the project settings under Build Settings and selecting bitcode to YES.

<img src="/static/app_thinning_bitcode_enable.png" alt="Drawing" style="width: 600px;"/>




## Exporting Your App for Testing (iOS, tvOS, watchOS)

Before uploading your app to iTunes Connect, optionally distribute it for testing on registered devices using an ad hoc provisioning profile or team provisioning profile. These distribution methods allow you to test variants of your app that are built locally by Xcode. Testers don’t need to be team members or iTunes Connect users to run the app, but their devices need to be registered in your developer account. You can register up to 100 devices per product family per year that your team uses for development and testing.

These are the steps to export your app for testing:

1. Register all test devices.
2. Archive your app.
3. Export the archive using either an ad hoc provisioning profile or team provisioning profile to code sign your app.
4. Install the app on test devices.
5. Solicit crash reports from testers.

What is ad hoc profile

An ad hoc provisioning profile is a distribution provisioning profile that allows your app to be installed on designated devices and to use app services without the assistance of Xcode. It’s one of the two types of distribution provisioning profiles that you can create for apps. (You use the other type of distribution provisioning profile later to submit your app to the store.)

### 1. Registering Test Devices

Register one or more test devices before you create an ad hoc or team provisioning profile. To register test devices, collect device IDs from testers and add them to your developer account.

### 2. Archiving Your App

Next, create an archive of your app. Xcode stores this archive in the Archives organizer.

###### To create an archive

 * In the Xcode project editor, choose a generic device—Generic iOS Device, Generic tvOS Device, or Generic iOS Device + watchOS Device—or your device name from the Scheme toolbar menu.
 You can’t create an archive of a simulator build. If a device is connected to your Mac, the device name appears in the Scheme toolbar menu. When you disconnect the device, the menu item changes to the generic device name.

 * Choose Product > Archive.
   The Archives organizer appears and displays the new archive.

Xcode runs preliminary validation tests on the archive and may display a validation warning in the project editor. If you see a warning, fix the issue and create the archive again.

### 3. Exporting Your App for Testing Outside the Store

*To create an iOS App file for testing*
 1. Open the Archives organizer (choose Organizer from the Window menu), and select the archive.

<img src="/static/app_thinning_archive_organizer.png" alt="Drawing" style="width: 600px;"/>


 2. Click the Export button, select an export option, and click Next.
    To distribute your app to users with designated devices, select “Save for Ad Hoc Deployment.” The app will be code signed with the distribution certificate.
    
    <img src="/static/app_thinning_createappstorepackage.png" alt="Drawing" style="width: 600px;"/>


 3. In the dialog that appears, choose a team from the pop-up menu and click Choose.
    If necessary, Xcode creates the needed signing identity and provisioning profile for you.
  
  <img src="/static/app_thinning_export_choose_team.png" alt="Drawing" style="width: 600px;"/>
    

 4. In the Device Support dialog, choose whether to export the universal app or a variant for a specific device, and click Next.
     * If you want to run the app on any supported device, select “Export one app for all compatible devices.”
     * If you want to test all device variances, select “Export for specific devices” and choose “All compatible device variants” from the pop-up menu.
     * If you want to test a specific device variant, select “Export a thinned app for a specific device” and choose the device family from the pop-up menu.
     
       <img src="/static/app_thinning_export_for_device.png" alt="Drawing" style="width: 600px;"/>


 5. In the dialog that appears, review the app, its entitlements, and the provisioning profile.


 6. Review the build options, and click Next.
  * If you use on-demand resources, check “Include manifest for over-the-air installation.”
  * If you distribute your app outside of the store, you need to host the on-demand resources yourself. The manifest file is an XML plist used by a device to find, download, and install apps from your web server.

  * If you want to test a build created from bitcode, check “Export from bitcode.”

  7. If you request a manifest file, enter details about your web server in the “Distribution manifest information” dialog that appears.

  Enter the following information:

  * **Name.** The name of the app displayed during download and installation.
  * **App URL.** A fully qualified HTTPS URL for the iOS App file.
  * **Display Image URL.** A fully qualified HTTPS URL for an app icon that is displayed during download and installation. The image file must be 57 x 57 pixels and in PNG format.
  * **Full Size Image URL.** A fully qualified HTTPS URL for a larger image that is displayed in iTunes. The image file must be 512 x 512 pixels and in PNG format.
  
      <img src="/static/app_thinning_enter_manifest_info.png" alt="Drawing" style="width: 600px;"/>

### 4. Installing Your App on Test Devices Using iTunes

To install the app on an iOS device using iTunes

1. Connect the testing device to a Mac running iTunes.
If possible, don’t use a Mac that you use for development. For watchOS apps, connect an iPhone paired with an Apple Watch.

2. Double-click the iOS App file that you created earlier.
3. In iTunes, click the device in the upper-left corner of the window.
4. Click the Apps button.

The app appears in the iTunes Apps list.

<img src="/static/app_thinning_installapp.png" alt="Drawing" style="width: 600px;"/>

5. Under Apps, choose “Sort by Name” or “Sort by Kind” from the pop-up menu.
An Install or Remove button appears adjacent to the app.

6. If an Install button appears, click it.
The button text changes to Will Install.

7. Click the Apply button or the Sync button in the lower-right corner to sync the device.
The app is uploaded to the device so that the user can start testing.

Finally, send the iOS App file to testers, along with the app installation instructions and the crash report instructions, as described in Soliciting Crash Reports from Testers.

## *How to check real App Store File Size*

If you are worried about the size of your App Store file, you can check using below steps

1. Go to iTunes Connect -> Your App -> Activity Tab
2. Go to the version you want to check and click on a build that you want to observe. There you have an option App Store File Sizes 

Following screenshot is an example, how size differ according to various devices.


<img src="/static/app_thinning_size_appstore.png" alt="Drawing" style="width: 600px;"/>
