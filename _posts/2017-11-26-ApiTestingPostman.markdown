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

Now let me tell you why this is important and you must adopt this, suppose you are creating an application then of course you must have a frontend, backend, testers and many more. There always comes a situation where some apis get fail either due to bad request or something else and to find that you always have to debug into your application to find the root cause.

 But via using postman scripts you will write the script once for the api and you can test it on one click and check it whether all the cases are "PASS" or "FAILED".

  If failure comes then there is a problem with the backend api or if all the cases has been passed then there must be a problem in frontend.

  And tester can also use it to check the bug belongs to frontend or backend.

**THIS WILL SAVE A LOT OF TIME** as you need to write the script once and even you can use that same script on your future apps.

So maybe first time when you're writing scripts may take time, but do not panic believe me it will save a lot of time later and more importantly you will get to know the root cause by just one click.

Assuming that you have the postman installed on your machine and you're familiar with it.

We are all set to move on :)

Although I suggest you to use your own apis, but if you do not have i am using the sample weather api for testing purpose. Here is the api link :

[Weather API](http://samples.openweathermap.org/data/2.5/weather?lat=35&lon=139&appid=b1b15e88fa797225412429c1c50c122a1)

And you can see the sample result below :-

<img src="/static/SampleApiHit_Postman.png" alt="Drawing" style="width: 600px;"/>

## Default Scripts

There are some pre defined scripts in the postman. So we will start from there.

Click on **Tests** to see the default scripts. Refer the image below:-

<img src="/static/Test_Postman.png" alt="Drawing" style="width: 600px;"/>

On the right side you can see there are several predefined options. Lets start, select **"Response body: Contains string"**.

<img src="/static/ResponseBody_Postman.png" alt="Drawing" style="width: 600px;"/>

Then click on **Send** and see the response on **Test Results**.

<img src="/static/TestFailResult_Postman.png" alt="Drawing" style="width: 600px;"/>

For now it will show failure as your json will not contain the default string. Now change the string which you need to find on json and hit **Send**. Now it will show **PASS** on the result.

<img src="/static/TestPassResult_Postman.png" alt="Drawing" style="width: 600px;"/>

Now lets take another example by checking the response time of your api. Select **"Response time is less than 200ms"** and click on **Send**. You can see the response below.

<img src="/static/ResponseResult_Postman.png" alt="Drawing" style="width: 600px;"/>

There are more predefined scripts. You can test one by one by yourself. It will help you to understand the javascript code.


## Writing your own custom scripts


Postman supports javascript for scripting. You do not need to worry if you do not know javascript. Lets see some example below, that would gave you confidence and some knowledge about javascript, it is pretty easy.

**Example 1**

Suppose you want to check any value from json. Lets say, in our wheather api there is a key **base** and we are going to check wheather it is equal to station or not. Find the code snippet below :-

<img src="/static/base_Postman.png" alt="Drawing" style="width: 600px;"/>

```swift
var jsonData = JSON.parse(responseBody);
var usersURL = "stations"
tests["Gets the correct users url"] = jsonData.base === usersURL;
```

Write above snipped on your postman test section and hit api. Refer the image below :-

<img src="/static/base_result_Postman.png" alt="Drawing" style="width: 600px;"/>

**Example 2**

You can test for any character or sentence using the below code snippet :

```
tests["Has correct updated text"] =
  responseBody.has("Type your text you want to search");
  ```

Now atleast, you can write some basic test cases using the above code snippets.


  Simply with little bit knowledge of javascript you can write some sweet test cases and make your life easier and safer.

  All the best :)
