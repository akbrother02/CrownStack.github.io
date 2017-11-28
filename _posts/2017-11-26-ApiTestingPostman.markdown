---
title:  "Api Testing via POSTMAN"
date:   2017-11-26
author: Ankit Jaiswal
categories:
- blog
tags:
- iOS
---

I guess we all are using POSTMAN or at least used once to test our api's. So we are quiet familiar with POSTMAN. This blog is all about writing Scripts to test api's on POSTMAN.

Now let me tell why this is important and you must adopt this, suppose you are creating a application of course you must have a frontend, backend, testers and many more. There always comes a situation where some apis get fail either due to bad request or something else and to find that you always have to debug into your application to find the root cause. But via using postman scripts you will write the script once for the api and you can test it on one click and check it whether all the cases are "PASS" or "FAILED". If failure comes then there is a problem with the backend api or if all the cases has been passed then there must be a problem in frontend. And tester can also use it to check the bug belongs to frontend or backend.

"THIS WILL SAVE A LOT OF TIME" as you need to write the script once and even you can use that same script on your future apps. So maybe first time when you're writing scripts may take time, but do not panic believe me it will save a lot of time later and more importantly you will get to know the root cause by just one click.

Assuming that you have the postman installed on your machine and you're familiar with it.

We are all set to move on :)

### Default Scripts

Although I suggest you to use your own apis, but if you do not have i am using the sample weather api for testing purpose. Here is the api link :

http://samples.openweathermap.org/data/2.5/weather?lat=35&lon=139&appid=b1b15e88fa797225412429c1c50c122a1

### Writing your own custom scripts
