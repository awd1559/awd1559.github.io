---
layout:     post
title:      "Android 目录"
subtitle:   " \"Android Resources\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - Android
---
><small>目录:[Android目录](/2014/06/09/android-index)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>

# Animation
## Property Animation
```
AnimatorSetR.animator.xxxx
@package:animator/xxx
<set
  android:ordering=["together" | "sequentially"]>
ObjectAnimator

    <objectAnimator
        android:propertyName="string"
        android:duration="int"
        android:valueFrom="float | int | color"
        android:valueTo="float | int | color"
        android:startOffset="int"
        android:repeatCount="int"
        android:repeatMode=["repeat" | "reverse"]
        android:valueType=["intType" | "floatType"]/>
ValueAnimator

    <animator
        android:duration="int"
        android:valueFrom="float | int | color"
        android:valueTo="float | int | color"
        android:startOffset="int"
        android:repeatCount="int"
        android:repeatMode=["repeat" | "reverse"]
        android:valueType=["intType" | "floatType"]/>

    <set>
        ...
    </set>
</set>
```

## View Animation
```
Tween animation
R.anim.xxx
@[package:]anim/xxxx
<?xml version="1.0" encoding="utf-8"?>
AnimationSet
<set
Interpolator xmlns:android="http://schemas.android.com/apk/res/android"
    android:interpolator="@[package:]anim/interpolator_resource"
    android:shareInterpolator=["true" | "false"] >
AlphaAnimation 
0-1
    <alpha
        android:fromAlpha="float"
        android:toAlpha="float" />
    <scale
ScaleAnimation
原大小是1
        android:fromXScale="float"
        android:toXScale="float"
        android:fromYScale="float"
        android:toYScale="float"
        android:pivotX="float"
        android:pivotY="float" />
    <translate
TranslateAnimation
100%相对于self
100%p相对于parent
        android:fromXDelta=“float|100%p"
        android:toXDelta="float"
        android:fromYDelta="float"
        android:toYDelta="float" />
    <rotate
RotateAnimation
        android:fromDegrees="float"
        android:toDegrees="float"
        android:pivotX="float"
        android:pivotY="float" />
    <set>
        ...
    </set>
</set>


//Frame animation
R.drawable.xxxx
@[package:]drawable.xxxx
<?xml version="1.0" encoding="utf-8"?>
AnimationDrawable
<animation-list xmlns:android="http://schemas.android.com/apk/res/android"
    android:oneshot=["true" | "false"] >
    <item
        android:drawable="@[package:]drawable/drawable_resource_name"
        android:duration="integer" />
</animation-list>
```

# ColorStateList
# Drawable
# Layout
# Menu
# String
# Style
# Misc


