---
title:  "Constraint Layout"
date:   2017-10-09
author: Ashutosh Singh
categories:
- blog
tags:
- android
---

One of the main goals of ConstraintLayout is to give you a way to efficiently create complex layouts with minimal nesting. It is alike `RelativeLayout`. ConstraintLayout is much powerful and versatile, aims to make developing layouts easier and faster while improving performance at runtime.

### Why do we need Constraint Layout?

`Speed` is the most important reason why we need ConstraintLayout. ConstraintLayout comes to avoid the nested ViewGroups in LinearLayouts and RelativeLayouts. Nesting can grow exponentially with each level of nesting. If the layout is too nested, layout time grows too large and app will start dropping frames, resulting in bad transitions. Easy to use.

### What are Constraint

The fundamental building block of ConstraintLayout is creating constraints. A constraint defines a relationship between two widgets in the layout and controls how those widgets will be positioned within the layout.The basic principles of how constraints work are very similar to how we create relationships between widgets in RelativeLayout.


<img src="/static/Screenshot_20171026-181127.png" alt="Drawing" style="width: 600px;"/>

We will create this layout by the regular layout(LinearLayouts). It structure will be like below. There is much nested `LinearLayout`. As we know that nested view decrease the performace at runtime.

```
<LinearLayout>
    <LinearLayout> </LinearLayout>
    <LinearLayout>
        <LinearLayout>  </LinearLayout>
        <LinearLayout>  </LinearLayout>
        <LinearLayout>  </LinearLayout>
    </LinearLayout>
</LinearLayout>
```

To resolve this we will create this layout using `ConstraintLayout`.

```
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <android.support.constraint.Guideline
        android:id="@+id/guideline"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_percent="0.45" />

    <ImageView
        android:id="@+id/image_view_header"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:contentDescription="@null"
        android:scaleType="centerCrop"
        android:src="@drawable/ic_login_header_bg"
        app:layout_constraintBottom_toTopOf="@+id/guideline"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <ImageView
        android:id="@+id/image_view_login_header_circle"
        android:layout_width="80dp"
        android:layout_height="80dp"
        android:contentDescription="@null"
        android:src="@drawable/ic_login_header_circle"
        app:layout_constraintBottom_toBottomOf="@+id/guideline"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        style="@style/textSize_large"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/log_in_to_your_account"
        android:textColor="@color/orai_blue"
        app:layout_constraintBottom_toTopOf="@+id/image_view_login_header_circle"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="@+id/image_view_header" />

    <ImageView
        android:id="@+id/image_view_fb_bg"
        android:layout_width="0dp"
        android:layout_height="40dp"
        android:layout_marginEnd="40dp"
        android:layout_marginStart="40dp"
        android:layout_marginTop="30dp"
        android:background="@color/orai_blue"
        android:contentDescription="@null"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/guideline" />

    <ImageView
        android:id="@+id/image_view_fb"
        android:layout_width="25dp"
        android:layout_height="25dp"
        android:contentDescription="@null"
        android:src="@drawable/ic_facebook"
        app:layout_constraintBottom_toBottomOf="@+id/image_view_fb_bg"
        app:layout_constraintHorizontal_chainStyle="packed"
        app:layout_constraintLeft_toLeftOf="@+id/image_view_fb_bg"
        app:layout_constraintRight_toLeftOf="@+id/text_view_facebook_login"
        app:layout_constraintTop_toTopOf="@+id/image_view_fb_bg" />

    <TextView
        android:id="@+id/text_view_facebook_login"
        style="@style/textSize_medium"
        android:layout_width="wrap_content"
        android:layout_height="25dp"
        android:layout_marginStart="15dp"
        android:text="@string/login_with_facebook"
        android:textColor="@color/white"
        app:layout_constraintBottom_toBottomOf="@+id/image_view_fb"
        app:layout_constraintHorizontal_chainStyle="packed"
        app:layout_constraintLeft_toRightOf="@+id/image_view_fb"
        app:layout_constraintRight_toRightOf="@+id/image_view_fb_bg"
        app:layout_constraintTop_toTopOf="@+id/image_view_fb" />

    <ImageView
        android:id="@+id/image_view_google_bg"
        android:layout_width="0dp"
        android:layout_height="40dp"
        android:layout_marginEnd="40dp"
        android:layout_marginStart="40dp"
        android:layout_marginTop="30dp"
        android:background="@drawable/bg_shadow"
        android:contentDescription="@null"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/image_view_fb_bg" />

    <ImageView
        android:id="@+id/image_view_google"
        android:layout_width="25dp"
        android:layout_height="25dp"
        android:src="@drawable/ic_google"
        app:layout_constraintBottom_toBottomOf="@+id/image_view_google_bg"
        app:layout_constraintHorizontal_chainStyle="packed"
        app:layout_constraintLeft_toLeftOf="@+id/image_view_google_bg"
        app:layout_constraintRight_toLeftOf="@+id/text_view_google_login"
        app:layout_constraintTop_toTopOf="@+id/image_view_google_bg" />

    <TextView
        android:id="@+id/text_view_google_login"
        style="@style/textSize_medium"
        android:layout_width="wrap_content"
        android:layout_height="25dp"
        android:layout_marginStart="10dp"
        android:text="@string/login_with_google"
        app:layout_constraintBottom_toBottomOf="@+id/image_view_google_bg"
        app:layout_constraintHorizontal_chainStyle="packed"
        app:layout_constraintLeft_toRightOf="@+id/image_view_google"
        app:layout_constraintRight_toRightOf="@+id/image_view_google_bg"
        app:layout_constraintTop_toTopOf="@+id/image_view_google_bg" />

    <ImageView
        android:id="@+id/image_view_email_bg"
        android:layout_width="0dp"
        android:layout_height="40dp"
        android:layout_marginEnd="40dp"
        android:layout_marginStart="40dp"
        android:layout_marginTop="30dp"
        android:background="@color/orai_blue"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/image_view_google_bg" />

    <ImageView
        android:id="@+id/image_view_email"
        android:layout_width="25dp"
        android:layout_height="25dp"
        android:src="@drawable/ic_email"
        app:layout_constraintBottom_toBottomOf="@+id/image_view_email_bg"
        app:layout_constraintHorizontal_chainStyle="packed"
        app:layout_constraintLeft_toLeftOf="@+id/image_view_email_bg"
        app:layout_constraintRight_toLeftOf="@+id/text_view_email_login"
        app:layout_constraintRight_toRightOf="@+id/image_view_email_bg"
        app:layout_constraintTop_toTopOf="@+id/image_view_email_bg" />

    <TextView
        android:id="@+id/text_view_email_login"
        style="@style/textSize_medium"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="10dp"
        android:text="@string/login_with_email"
        android:textColor="@color/white"
        app:layout_constraintBottom_toBottomOf="@+id/image_view_email_bg"
        app:layout_constraintHorizontal_chainStyle="packed"
        app:layout_constraintLeft_toRightOf="@+id/image_view_email"
        app:layout_constraintRight_toRightOf="@+id/image_view_email_bg"
        app:layout_constraintTop_toTopOf="@+id/image_view_email_bg" />
</android.support.constraint.ConstraintLayout>
```
