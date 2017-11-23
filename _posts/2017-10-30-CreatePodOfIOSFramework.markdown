---
title:  "CocoaPod of ios framework"
date:   2017-10-30
author: Ankit Jaiswal
categories:
- blog
tags:
- iOS
---

CocoaPods is the dependency manager for Objective-C/Swift projects. It has thousands of libraries and can help you scale your projects elegantly.

Dependencies for projects are specified in a single text file called 'Podfile' which CocoaPods resolve dependencies between libraries, fetch the resulting source code, then link it together in an Xcode workspace to build your project.

Till now you have only used dependencies of others. So what about making your own. So lets start :)

I am supposing that you have the framework ready and you want to share your framework to your teammates via CocoaPod.

So the first step is publishing your framework to GitHub.

### Pushing to GitHub

CocoaPods needs a source for the Pod. In our case, we use GitHub for this. I will quickly go through the necessary steps to push your project to GitHub.

In brief, here is what you need to do:

1. Create a repository on Github. Call it "Your Pod Name or Project Name".
2. Copy the URL to your repository.
3. In Terminal, navigate to your project.
4. Initialize Git: git init
5. Add the changes: git add .
6. Commit the changes: git commit -m "init"
7. Add a remote origin: git remote add origin <paste your URL here>
8. Push your commit: git push -u origin master.

Your code has been pushed to a git repository.

Now you must create a release for your repository. A release is a new version of your product. You can create one in your GitHub dashboard. Navigate to your repository on GitHub.

1.Click the releases button on project home.

<img src="/static/CocoaPod_release.png" alt="Drawing" style="width: 600px;"/>

2.Click Create a new release as shown below.

<img src="/static/CocoaPod_new_release.png" alt="Drawing" style="width: 600px;"/>

3.Set the version number to 0.1.0 or any you want, then set a title and description for the release.

<img src="/static/CocoaPod_version.png" alt="Drawing" style="width: 600px;"/>

4.Click Publish release and you should get something like this:

<img src="/static/CocoaPod_publish.png" alt="Drawing" style="width: 600px;"/>

Its all done with GitHub. Now need to deploy our code on CocoaPod.

### Creating Your Own Pod

I suppose you have the POD installed on your mac or you can installed it using the below command :

sudo gem install cocoapods --pre


### Creating a Podspec for your project

Follow the following steps to create podspec :-

1. Navigate to your project file in the Terminal.
2. Run the following command to create the file: touch YOURPROJECTNAME.podspec.
3. Now open the file using an editor.
4. Paste the following code inside the Podspec.

Pod::Spec.new do |s|
  s.name             = 'PODFRAMEWORK'
  s.version          = '0.0.1'
  s.summary          = 'Your project summary.'

  s.description      = <<-DESC
Write your project description here
                       DESC

  s.homepage         = 'https://github.com/<YOUR USERNAME>/PODFRAMEWORK'
  s.license          = { :type => 'MIT', :file => 'LICENSE' }
  s.author           = { 'YOUR NAME' => 'yourEmail' }
  s.source           = { :git => 'https://github.com/<YOUR USERNAME>/PODFRAMEWORK.git', :tag => s.version.to_s }

  s.ios.deployment_target = '10.0'
  s.source_files = 'PODFRAMEWORK/*'

end

The above variables of CocoaPod after 's' is the required fields. We need to fill all the required variables.

Lets find the explanation below :-

1. s.name - It is the name of the pod which others use to add to their project.

2. s.version - This is the version of your pod which we had released above in the github.
Note: Version number must match to your github release otherwise it will give error while validating.

3. s.summary - Write your project summary, this will get displayed on the CocoaPod website.

4. s.description - Write your project description, this will also get displayed on the CocoaPod website.
Note : Make sure that the description is longer than the summary otherwise you will encounter a warning while validating.

5. s.homepage - It is the home URL for the Pod. Make sure to replace YOUR GITHUB USERNAME with your username.

6. s.author - Write the developers name here.

7. s.source - Fill your github repository source url.

8. s.source_files - This is tricky one and most important. It tells CocoaPods which files you need to clone. Lets take one example to understand this :

Suppose you have project where source file name is 'PODFRAMEWORK' and inside that you want to provide all the swift files to user so you will simply give source url as :

'PODFRAMEWORK/*.swift'

where * indicates any file can be used.

Say you want all the files in /PODFRAMEWORK to be included when the Pod is installed. Just put an asterisk instead of the file name and type:

'PODFRAMEWORK/*'

This will include each and every file inside 'PODFRAMEWORK' directory.

### Linting The CocoaPod Project

Now CocoaPod will verify that nothing is wrong in your project as per there norms. This may produce some errors and warnings if you have not followed this tutorial carefully. But do not panic :).

Now lets lint your project. Navigate to your project directory and run the below command :-

pod lib lint

you may encounter some warnings or error as below :

<img src="/static/pod_lib_lint_warning.png" alt="Drawing" style="width: 600px;"/>

 For warnings it will guide you to add --allow-warnings like this :

pod lib lint --allow-warnings

For error, you can use github issues section to check and rectify your problem but if you have followed the above points carefully you will not face any kind of error.

<img src="/static/pod_lib_lint_validation_success.png" alt="Drawing" style="width: 600px;"/>


###  Publishing Your Pod

Cheers its time to publish your pod to other developers. Everything is good till now. Now you need to trunk your account via CocoaPod. Trunk is actually not validating your account it is just creating session. You do not need any password here just need an email and then type the below command :-

pod trunk register <Your Email>

Goto your email and click on the link provided by CocoaPod. Now its all done we just need to publish our pod.

### Pushing Your Pod

All that is left is to push your podspec using Trunk to CocoaPods:

pod trunk push YOURPROJECTNAME.podspec

You will get the success message as shown below :-

<img src="/static/final_success.png" alt="Drawing" style="width: 600px;"/>

Oh Finally we did it, Now you can share your pod to your developers.
