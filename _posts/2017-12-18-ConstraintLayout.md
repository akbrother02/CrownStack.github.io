---
layout: post
title: "Constraint Layout"
categories:
- blog
tags:
- android
author: Prinsu Kumar
---


Added app:layout_constra1intTop_toTopOf="parent"  in textview for top of view.
Added         app:layout_constraintLeft_toLeftOf="parent" for top left of view.

If you want to center a textview horizontally you can use below:
app:layout_constraintLeft_toLeftOf="parent"
app:layout_constraintRight_toRightOf="parent"
and want to relate with another view like below an imageview you can use:
app:layout_constraintTop_toBottomOf="@+id/image_view_profile"


If you want to add two view horizontally then set first view like below:

set app:layout_constraintLeft_toLeftOf="parent"

<TextView
    android:id="@+id/text_view_email"
    android:layout_width="wrap_content"
    android:layout_height="40dp"
    android:layout_marginStart="10dp"
    android:layout_marginTop="10dp"
    android:gravity="center"
    android:text="Email"
    app:layout_constraintLeft_toLeftOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/text_view_name" />


and second view like below:

set app:layout_constraintEnd_toStartOf="parent"
app:layout_constraintLeft_toRightOf="parent"

<EditText
     android:id="@+id/edit_text_password"
     android:layout_width="220dp"
     android:layout_height="40dp"
     android:layout_marginTop="10dp"
     android:hint="Password"
     android:paddingLeft="10dp"
     app:layout_constraintEnd_toStartOf="parent"
     app:layout_constraintLeft_toRightOf="parent"
     app:layout_constraintTop_toBottomOf="@+id/edit_text_name" />





  If you want to set a view in bottom of screen use these lines of code below:

  set   app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toRightOf="parent"
        app:layout_constraintRight_toLeftOf="parent"

 Ex:       
 <Button
        android:layout_width="200dp"
        android:layout_height="wrap_content"
        android:layout_marginBottom="10dp"
        android:layout_marginTop="30dp"
        android:background="@android:color/holo_blue_dark"
        android:text="Save"
        android:textColor="@android:color/white"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toRightOf="parent"
        app:layout_constraintRight_toLeftOf="parent" />
