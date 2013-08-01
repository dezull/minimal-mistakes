---
layout: post
title: Overlaying View in Android
modified: 2013-08-02
category: articles
tags: [code, android]
comments: true
---

Here is what I want to achieve, overlaying a View, on top of another View. See below screenshot, which is quite similar to the Facebook profile page for Android/IOS apps. Out of laziness, I put the grayish blue background instead of a cover photo for the header.

![Android screenshot]({{ site.url }}/assets/post-images/android-overlay-view.png)

So I want to put the icon, surrounded by a blue border, which is overlaid on top of another View (or Views!). Luckily, RelativeLayout allows us to position the contained View on top of another. Just make sure the overlaying View is declared after the overlaid View inside the layout xml.

{% highlight xml %}
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    tools:ignore="HardcodedText,ContentDescription" >

    <RelativeLayout
        android:id="@+id/header"
        android:layout_width="match_parent"
        android:layout_height="250dp"
        android:layout_alignParentLeft="true"
        android:layout_alignParentTop="true"
        android:background="#C8CFD5" />

    <!--
    The icon, we overlay this on top of the @id/header, and offsetting it 214dp from the top.
    We need to put it in the center of @id/iconContainer below.
    -->
    <ImageView
        android:id="@+id/icon"
        android:layout_width="72dp"
        android:layout_height="80dp"
        android:layout_alignParentLeft="true"
        android:layout_alignParentTop="true"
        android:layout_marginLeft="20dp"
        android:layout_marginTop="214dp"
        android:background="#ffffff"
        android:scaleType="fitXY"
        android:src="@drawable/ic_launcher" />

    <!--
    Icon container, its height is 80dp, which includes its background drawable 4dp stroke.
    We need to also overlay this on top of @id/header.
    Which means the content's height is actually 72dp, similar to the icon.
    So from the top, we should offset it by 214dp(@id/icon offset) - 4dp(stroke) = 210dp.
    Similar formula is applied to the left margin, 20dp(@id/icon offset) - 4dp(stroke) = 16dp
    -->
    <FrameLayout
        android:id="@+id/iconContainer"
        android:layout_width="80dp"
        android:layout_height="80dp"
        android:layout_alignParentLeft="true"
        android:layout_alignParentTop="true"
        android:layout_marginLeft="16dp"
        android:layout_marginTop="210dp"
        android:background="@drawable/shape_agency_logo_holder" >
    </FrameLayout>

    <TextView
        android:id="@+id/label"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/header"
        android:layout_marginLeft="16dp"
        android:layout_marginTop="16dp"
        android:layout_toRightOf="@+id/iconContainer"
        android:text="Awesome Guy" />

</RelativeLayout>
{% endhighlight  %}

There it is. I wish it was simpler.
