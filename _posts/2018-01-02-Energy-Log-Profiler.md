---
title:  "Energy Log with Instruments"
date:   2018-01-02
author: Sagar Kumar
categories:
- blog
tags:
- iOS
---

`Instruments` is Apple's premiere tool for analyzing the performance of iOS and OS X applications.

### When to Use Instruments
* While testing your app with Xcode, consult the debug navigator gauges from Xcode menu(`View\Navigators\Show Debug Navigator`) before diving into Instruments. These gauges provide high-level information about your app’s CPU, memory, energy usage, and more. Often, they provide all the information you need to improve performance and resolve common problems quickly. Use Instruments when you need to perform more detailed analysis.

    <img src="/static/navigators_showdebug.png" alt="Drawing" style="width: 600px;"/>

### System Requirements
* Instruments is installed with Xcode. If you don’t already have Xcode installed, download it from the Mac App Store.

* If you plan to profile an app on an iOS device, you’ll need to provision your device. See [How to launch app on devices.](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/LaunchingYourApponDevices/LaunchingYourApponDevices.html#//apple_ref/doc/uid/TP40012582-CH27)


### How to open `Instruments` in Xcode.
* From Xcode's menu bar, select `Xcode\Open Developer Tool\Instruments`.

    <img src="/static/openDevTools_intruments.png" alt="Drawing" style="width: 600px;"/>

* From Xcode’s menu bar, select `Product\Profile`, or press `⌘I`. This will build the app and launch `Instruments`.

    <img src="/static/product_profile_intruments.png" alt="Drawing" style="width: 600px;"/>

* Click and hold the Run button in the Xcode toolbar and choose Profile.

* After done above things you'll get a selection window(screen) like this:

    <img src="/static/instrumets_screen.png" alt="Drawing" style="width: 600px;"/>


### Measure Energy Impact
Use the Energy Log profiling to monitor a variety of factors that affect energy usage on an iOS device, including CPU activity, network activity, screen brightness, and more.

##### To monitor the energy impact of an iOS app
* Launch Instruments, and create a new trace document that targets your device and app with the Energy Log profiling template.

* Click the Record button, or press Command-R to begin recording a trace

  <img src="/static/startRecord.png" alt="Drawing" style="width: 600px;"/>

  For best results, consider performing the trace wirelessly.
  Doing so allows you to more accurately profile the device in
  a real-world scenario—on battery power, with accelerometers,
  and so on. To learn how to enable wireless device profiling, see [Target an iOS Device Wirelessly.](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/WorkingwithTargets.html#//apple_ref/doc/uid/TP40004652-CH10-SW5)

* Use the app normally on the device, while allowing energy data to be collected.

* Click the Stop button, or press Command-R again, when complete.

* Go through the collected data and look for spikes or areas of otherwise unusual or unexpected activity. Then, review the code in these areas to determine whether improvements can be made.

    <img src="/static/energy_ statistics.png" alt="Drawing" style="width: 600px;"/>

* The Energy Usage instrument indicates a level from 0 to 20, indicating how much energy your app is using at any given time. These numbers are subjective.

* If your app’s energy usage level is occasionally high, it doesn’t necessarily mean that your app has a problem. Your app may simply require more energy for some of the tasks it performs. For example, it may use the GPS while performing complex network operations. This is valid energy use. What you should look for are spikes or areas of high energy use that are unexpected or that could be performed at more optimal times.

##### Log Energy Usage Directly on an iOS Device
* We can log energy-related data under normal use in order to take realistic measurements.

* With energy logging enabled, your iOS device records energy-related data unobtrusively while the device is used. Because logging is efficient, you can log all day.

* Logging continues even while the device is in sleep mode. However, if the device’s battery drains completely or the iOS device is powered off, the log data is lost.

  ###### These are following steps to log energy data in iOS Device
  1. Go to Settings > Developer > Logging on your device.

      <img src="/static/settings.png" alt="Drawing" style="width: 400px;"/>

      <img src="/static/settings_developer.png" alt="Drawing" style="width: 400px;"/>

  2. Enable energy logging.

    <img src="/static/settings_dev_instruments.png" alt="Drawing" style="width: 400px;"/>

  3. Start recording with device.

    <img src="/static/startrecording.png" alt="Drawing" style="width: 400px;"/>

  4. Use your device normally.

  5. When you’re done, return to Settings > Developer > Logging and tap Stop Recording.

    <img src="/static/startrecording.png" alt="Drawing" style="width: 400px;"/>

##### How to import logged energy data from an iOS device to Mac.

  1. Launch Instruments, and create a new trace document that targets your device and app with the Energy Log profiling template.

  2. From Instruments Menu bar, Choose File > Import Logged Data from Device.
