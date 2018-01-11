---
layout: post
title: "Constraint Layout"
categories:
- blog
tags:
- android
author: Prinsu Kumar
---

## ConstraintLayout:

As provided by Xaver Kapeller - "The main purpose of the ConstraintLayout is to fix problems with the RelativeLayout, and it does it so well. You can do so many things that were impossible with a RelativeLayout.

    `Constraint Layout: This new layout is a flexible layout manager for your app that allows you to create dynamic user interfaces without nesting multiple layouts. It is distributed as a support library that is tightly coupled with Android Studio and backwards compatible to API Level 9`.

    `At first glance, Constraint Layout is similar to RelativeLayout. However, the Constraint Layout was designed to be used in Studio and it can efficiently express your app design so that you rely on fewer layouts like LinearLayout, FrameLayout, TableLayout, or GridLayout. Lastly, with the built-in automatic constraints inference engine. You can freely design your UI to your liking and let Android Studio do the hard work`.

<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fillViewport="true"
    tools:context="constraint.com.constraintlayoutdemo.MainActivity">

    <android.support.constraint.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:minHeight="600dp">

        <TextView
            android:id="@+id/text_view_cancel"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginStart="10dp"
            android:layout_marginTop="16dp"
            android:text="Cancel"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintTop_toTopOf="parent" />

        <de.hdodenhof.circleimageview.CircleImageView
            android:id="@+id/image_view_profile"
            android:layout_width="90dp"
            android:layout_height="90dp"
            android:layout_centerHorizontal="true"
            android:layout_marginTop="20dp"
            android:src="@drawable/ic_launcher_background"
            app:layout_constraintLeft_toRightOf="parent"
            app:layout_constraintRight_toLeftOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/text_view_cancel" />

        <TextView
            android:id="@+id/text_view_change_image"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="8dp"
            android:text="Change Image"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/image_view_profile" />

        <TextView
            android:id="@+id/text_view_name"
            android:layout_width="85dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:gravity="center_vertical|left"
            android:text="Name"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/text_view_change_image" />

        <EditText
            android:id="@+id/edit_text_name"
            android:layout_width="220dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:hint="Name"
            android:paddingLeft="10dp"
            app:layout_constraintEnd_toStartOf="parent"
            app:layout_constraintLeft_toRightOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/text_view_change_image" />

        <TextView
            android:id="@+id/text_view_email"
            android:layout_width="85dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:gravity="center_vertical|left"
            android:text="Email"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/text_view_name" />

        <EditText
            android:id="@+id/edit_text_email"
            android:layout_width="220dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:hint="Email"
            android:inputType="textEmailAddress"
            android:paddingStart="10dp"
            app:layout_constraintEnd_toStartOf="parent"
            app:layout_constraintLeft_toRightOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/edit_text_name"
            tools:ignore="RtlSymmetry" />

        <TextView
            android:id="@+id/text_view_password"
            android:layout_width="85dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:gravity="center_vertical|left"
            android:text="Password"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintLeft_toRightOf="@+id/edit_text_password"
            app:layout_constraintTop_toBottomOf="@+id/text_view_email" />

        <EditText
            android:id="@+id/edit_text_password"
            android:layout_width="220dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:hint="Password"
            android:inputType="textPassword"
            android:paddingStart="10dp"
            app:layout_constraintLeft_toRightOf="parent"
            app:layout_constraintRight_toLeftOf="@+id/text_view_password"
            app:layout_constraintTop_toBottomOf="@+id/edit_text_email"
            tools:ignore="RtlSymmetry" />

        <TextView
            android:id="@+id/text_view_profession"
            android:layout_width="85dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:gravity="center_vertical|left"
            android:text="Profession"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintLeft_toRightOf="@+id/edit_text_profession"
            app:layout_constraintTop_toBottomOf="@+id/text_view_password" />

        <EditText
            android:id="@+id/edit_text_profession"
            android:layout_width="220dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:hint="Profession"
            android:inputType="textPassword"
            android:paddingStart="10dp"
            app:layout_constraintLeft_toRightOf="parent"
            app:layout_constraintRight_toLeftOf="@+id/text_view_profession"
            app:layout_constraintTop_toBottomOf="@+id/edit_text_password" />

        <TextView
            android:id="@+id/text_view_phone"
            android:layout_width="85dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:gravity="center_vertical|left"
            android:text="Phone:"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/text_view_profession" />

        <EditText
            android:id="@+id/edit_text_phone"
            android:layout_width="220dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:hint="Phone"
            android:inputType="phone"
            android:paddingStart="10dp"
            app:layout_constraintEnd_toStartOf="parent"
            app:layout_constraintLeft_toRightOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/edit_text_profession"
            tools:ignore="RtlSymmetry" />

        <TextView
            android:id="@+id/text_view_fax"
            android:layout_width="85dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:gravity="center_vertical|left"
            android:text="Fax:"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/text_view_phone" />

        <EditText
            android:id="@+id/edit_text_fax"
            android:layout_width="220dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:hint="Fax"
            android:inputType="number"
            android:paddingStart="10dp"
            app:layout_constraintEnd_toStartOf="parent"
            app:layout_constraintLeft_toRightOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/edit_text_phone"
            tools:ignore="RtlSymmetry" />

        <TextView
            android:id="@+id/text_view_city"
            android:layout_width="85dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:gravity="center_vertical|left"
            android:text="City:"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/text_view_fax" />

        <EditText
            android:id="@+id/edit_text_city"
            android:layout_width="220dp"
            android:layout_height="40dp"
            android:layout_marginStart="10dp"
            android:layout_marginTop="10dp"
            android:hint="City"
            android:inputType="text"
            android:paddingStart="10dp"
            app:layout_constraintEnd_toStartOf="parent"
            app:layout_constraintLeft_toRightOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/edit_text_fax"
            tools:ignore="RtlSymmetry" />

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
    </android.support.constraint.ConstraintLayout>
</ScrollView>
