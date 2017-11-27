---
layout: post
title: "Dynamic Linking"
categories:
- blog
tags:
- UI
author: Prinsu Kumar
---

Firebase is such an exciting new collection of services that I have been reading.
Now lets cover the feature of `Firebase` to learn excatly how we can use `Firebase Dynamic Links`.
It allow us to provide deep links that have ability to survive the installation process and more.
Ex: Suppose you want to link the user to a specific screen in our app from an external source, then
you can create a deep link to achieve this functionality.

Note: Suppose user doesn't have our app installed, in this case deep links would not work.
Then Firebase features what are called `Dynamic Links` these links are as same as deep links,
except they are able to provide the install process. So if the user clicks one of these links without
having our app installed, it will take up to install the app from `Google play store` or your custom app link
and after completion it will
navigate you to the deep link that has been assigned to `Dynamic link`.

### Hold context across application install

If the user clicks the dynamic link and the link requires your application to be installed,
then link will be opened directly once the application has been installed.

### Hold context across application upgrades

if the clicked dynamic link requires an upgraded version,
then it will handle the dynamic link once the application has finished installing.

### Behave just like normal links

In case the application doesn't require installation(if already installed) then clicking the dynamic link
will automatically open the desired screen.
Now if something is remaining, we can integrate Dynamic Links with Firebase Analytics to track the
interaction with any links that we generate for our applications.
But if we require only simple tracking, then we can use the automatic built-in analytics from the
Dynamic Links panel within Firebase Console where we can collect interacted links.
Deep linking is a technology that closes the gap between multiple platforms.

For example: Suppose your friend has emailed or shared some youtube video to you.
When you are on `web platform` , you click on that url and it will simply navigate you
to the youtube video. But in mobile, If you have configured `deep linking` in your app,
When you click on the link, It will ask you to open that link either in browser,
youtube or some other app that is also configured to handle youtube video urls.

### Why Deep Linking ?

Link Name: This is the name which you will be using to define the link,
make sure it should short and descriptive.

Link URL: The deep link in which the application will open for this link.

There are multiple use cases. Some of them are:

## Converting web users to App users:

When a user shares a link from your web app, you can generate deep link for it.
So when the user open that link on different device,
they will automatically redirected to your app.

## To increase user experience:

Suppose the user was browsing your app and decides to email the link to itself.
If user have your app installed, it will automatically be navigated to that content
that he was previously browsing.

