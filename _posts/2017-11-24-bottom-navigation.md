---
layout: post
title: "Bottom Navigation"
categories:
- blog
tags:
- android

author: Prinsu Kumar
---

Bottom navigation provides quick access to top-level views of an app. It is primarily designed for use on mobile. Larger displays, like desktop, may achieve a similar effect by using side navigation. There has historically been much discussion around navigation in Android. In earlier versions of Android, bottom navigation was a very popular navigational design pattern, but there was a growing concern that using this pattern in Android was too similar to navigation in iOS. During this period, Android was still trying to distinguish itself as a major mobile platform and it strove to be completely different than iOS. The solution? Google introduced the navigation drawer. The downfall to the navigation drawer is that it hides the user’s navigation options in this side drawer that is not visible to the user.

I have used it in my current project. I had no idea that Google was bringing bottom navigation back into Android.
The documentation is great and the demos are awesome! Google recently released v25 of the Android Design Library with support for the bottom navigation bar. The purpose of this blog is to demonstrate a simple implementation of bottom navigation in Android. Let’s begin!

Setup and Usage

After creating a new project in Android Studio you must import the dependency for the Android Design Library.

### app/build.gradle

```
dependencies {
     compile 'com.android.support:appcompat-v7:25.0.0'
     compile 'com.android.support:design:25.0.0'
     compile 'com.android.support:support-v4:25.0.0'
 }
 These are pretty standard dependencies for any Android application. The dependencies declared here are for the Android AppCompat Library, Android Support Design Library, and the Android Support Library.

```
 Next, a layout needs to be created for the MainActivity.

 ```
 <?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.credera.bottomnavigation.MainActivity">
        <include layout="@layout/include_main_content" />
        <android.support.design.widget.BottomNavigationView
            android:id="@+id/bottom_navigation_menu"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_alignParentBottom="true"
            app:itemBackground="@color/colorPrimary"
            app:itemIconTint="@android:color/white"
            app:itemTextColor="@android:color/white"
            app:menu="@menu/bottom_nav_menu"/>
</RelativeLayout>

```

This is a pretty standard activity layout in which the main content of the activity is separated into its own layout file and then included in the parent layout. The difference here is that the layout contains the BottomNavigationView from the Android Support Design Library. After providing some standard Android layout attributes you have to apply view-specific attributes.

* app:itemBackground – Background color of each item in the navigation bar.
* app:itemIconTint   – Color of the icon used for each navigation item.
* app:itemTextColor  – Color of the text used to describe each item.
* app:menu           – Menu resource file that creates each navigation item.

One consideration here would be using a ColorStateList for the itemIconTint and itemTextColor. This would allow you to provide different colors for enabled and disabled states.

Next, let’s have a look at the bottom_nav_menu.xml resource file that creates all of the items for our bottom navigation bar.

```
<?xml version="1.0" encoding="utf-8"?>
<menu
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/menu_home_item"
        android:title="@string/menu_home_text"
        android:icon="@drawable/ic_home_white_24dp"
        android:enabled="true"
        app:showAsAction="ifRoom" />
    <item
        android:id="@+id/menu_locations_item"
        android:title="@string/menu_locations_text"
        android:icon="@drawable/ic_location_on_white_24dp"
        android:enabled="true"
        app:showAsAction="ifRoom" />
    <item
        android:id="@+id/menu_menu_item"
        android:title="@string/menu_menu_text"
        android:icon="@drawable/ic_restaurant_menu_white_24dp"
        android:enabled="true"
        app:showAsAction="ifRoom" />
</menu>
```

Each item is given an ID for referencing in code, a title to describe the item, an icon to provide a visual representation of the item, and an enabled state. All items are given the app:showAsAction=”ifRoom” attribute which will show the item if room is available. Since bottom navigation bars are only supposed to contain three to five items, we can safely assume that all of our items will show.

To finish our demonstration, we need to set up our Main Activity and the fragments associated with each navigation item. Our `BottomNavigationView` logic is isolated to the MainActivity.

```
public class MainActivity extends AppCompatActivity {

 private  mBottomNavigationView;

 @Override
 protected void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);

  setContentView(R.layout.activity_main);
  BottomNavigationView();
 }

 private void BottomNavigationView() {
   // Retrieve a reference to the bottom navigation view.
   mBottomNavigationView = (BottomNavigationView) findViewById(R.id.bottom_navigation_menu);
   mBottomNavigationView.setOnNavigationItemSelectedListener(mItemSelectedListener);
   // Launch initial fragment.
   getSupportFragmentManager().beginTransaction()
    .add(R.id.content_container, HomeFragment.newInstance(), HomeFragment.TAG)
    .addToBackStack(null)
    .commit();
 }

 // Create navigation item selected click listener.

 private BottomNavigationView.OnNavigationItemSelectedListener mItemSelectedListener =
  new BottomNavigationView.OnNavigationItemSelectedListener() {
   @Override
   public boolean onNavigationItemSelected(@NonNull final MenuItem item) {
    final FragmentManager supportFragmentManager = getSupportFragmentManager();
    switch (item.getItemId()) {
     // Launch Home Fragment.
     case R.id.menu_home_item:
      final Fragment homeFragment = supportFragmentManager.findFragmentByTag(HomeFragment.TAG);
      if (homeFragment == null) {
       supportFragmentManager.beginTransaction()
        .replace(R.id.content_container, HomeFragment.newInstance(), HomeFragment.TAG)
        .addToBackStack(null)
        .commit();
      } else {
       supportFragmentManager.beginTransaction()
        .replace(R.id.content_container, homeFragment)
        .addToBackStack(null)
        .commit();
      }
      break;

     // Launch Locations Fragment.
     case R.id.menu_locations_item:
      final Fragment locationsFragment = supportFragmentManager.findFragmentByTag(LocationsFragment.TAG);
      if (locationsFragment == null) {
       supportFragmentManager.beginTransaction()
        .replace(R.id.content_container, LocationsFragment.newInstance(), LocationsFragment.TAG)
        .addToBackStack(null)
        .commit();
      } else {
       supportFragmentManager.beginTransaction()
        .replace(R.id.content_container, locationsFragment)
        .addToBackStack(null)
        .commit();
      }
      break;

     // Launch Menu Fragment.    
     case R.id.menu_menu_item:
      final Fragment menuFragment = supportFragmentManager.findFragmentByTag(MenuFragment.TAG);
      if (menuFragment == null) {
       supportFragmentManager.beginTransaction()
        .replace(R.id.content_container, MenuFragment.newInstance(), MenuFragment.TAG)
        .addToBackStack(null)
        .commit();
      } else {
       supportFragmentManager.beginTransaction()
        .replace(R.id.content_container, menuFragment)
        .addToBackStack(null)
        .commit();
      }
      break;
    }

    return false;
   }
  };
}
```
The HomeFragment is being launched initially and then any time a navigation item is chosen, the current fragment will be swapped for the new fragment. If you are not familiar with fragments and fragment transactions, check out the Android Developer’s training guide for fragments. I have left out the code for the fragments since they only contain a TextView for each screen.

### CONCLUSION

Bottom navigation brings another way of designing navigation for Android apps. When used correctly, this new style of navigation looks amazing in apps using material design. Developers should use the bottom navigation flow to facilitate easy and visible navigation for the user. 
