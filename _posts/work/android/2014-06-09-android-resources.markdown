---
layout:     post
title:      "Android Resources"
subtitle:   " \"Android Resources\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - Android
---
><small>目录:[Android目录](/2014/06/09/android)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>

# [Animation]((https://developer.android.google.cn/guide/topics/resources/animation-resource.html))

#### Property Animation
> - change object's properties over a set amount of time
> - since api 11
> - 
> - store at res/animator/filename.xml
> - ref In Java: R.animator.filename
> - ref In XML: @[package:]animator/filename
> - 
> - <animator>        => ValueAnimator
> - <objectAnimator>  => ObjectAnimator
> - <set>             => AnimatorSet

```
<set
  android:ordering=["together" | "sequentially"]>

    <objectAnimator
        android:propertyName="string"
        android:duration="int"              
        android:valueFrom="float | int | color"
        android:valueTo="float | int | color"
        android:startOffset="int"
        android:repeatCount="int"
        android:repeatMode=["repeat" | "reverse"]
        android:valueType=["intType" | "floatType"]/>

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

> - load Property Animator in Java

```
AnimatorSet set = (AnimatorSet) AnimatorInflater.loadAnimator(myContext, R.anim.property_animator);
set.setTarget(myObject);
set.start();
```






#### View Animation
> - store at res/anim/filename.xml
> - ref In Java: R.anim.filename
> - ref In XML: @[package:]anim/filename
> - 
> - <set>       => AnimationSet
> - <alpha>     => AlphaAnimation: 0 ~ 1
> - <scale>     => ScaleAnimation: 1 ~ 
> - <translate> => TranslateAnimation: 100%相对于self, 100%p相对于parent
> - <rotate>    => RotateAnimation


> - Tween animation

```
<?xml version="1.0" encoding="utf-8"?>
AnimationSet
<set
Interpolator xmlns:android="http://schemas.android.com/apk/res/android"
    android:interpolator="@[package:]anim/interpolator_resource"
    android:shareInterpolator=["true" | "false"] >
    <alpha
        android:fromAlpha="float"
        android:toAlpha="float" />
    <scale
        android:fromXScale="float"
        android:toXScale="float"
        android:fromYScale="float"
        android:toYScale="float"
        android:pivotX="float"
        android:pivotY="float" />
    <translate
        android:fromXDelta=“float|100%p"
        android:toXDelta="float"
        android:fromYDelta="float"
        android:toYDelta="float" />
    <rotate
        android:fromDegrees="float"
        android:toDegrees="float"
        android:pivotX="float"
        android:pivotY="float" />
    <set>
        ...
    </set>
</set>
```

> - load View Animation in Java

```
ImageView image = (ImageView) findViewById(R.id.image);
Animation hyperspaceJump = AnimationUtils.loadAnimation(this, R.anim.hyperspace_jump);
image.startAnimation(hyperspaceJump);
```


> - Interpolators
> - store at res/anim/filename.xml
> - ref In XML: @[package:]anim/filename

```
<?xml version="1.0" encoding="utf-8"?>
<InterpolatorName xmlns:android="http://schemas.android.com/apk/res/android"
    android:attribute_name="value"
    />
```

> - Frame animation
> - store at res/drawable/filename.xml
> - ref in XML R.drawable.xxxx
> - ref in Java @[package:]drawable.xxxx

```
<?xml version="1.0" encoding="utf-8"?>
<animation-list xmlns:android="http://schemas.android.com/apk/res/android"
    android:oneshot=["true" | "false"] >
    <item
        android:drawable="@[package:]drawable/drawable_resource_name"
        android:duration="integer" />
</animation-list>
```


```
AnimationDrawable mAnimationDrawable = new AnimationDrawable();
for(){
    nDrawable = getResources().getDrwable(R.drawable.drawable_anim);
    mAnimationDrawable.addFrame(nDrawable);
}
mAnimationDrawable.setOneShot(false);
mAnimationDrawable.start();




//as background of view
ImageView iv = (ImageView)findViewById(R.id.iv);
iv.setBackgroundResource(R.anim.frame_ani);
AnimationDrawable ad = (AnimationDrawable)iv.getBackground();
ad.start();
```











# ColorStateList
> - store at res/color/filename.xml
> - ref In Java: R.color.filename
> - ref In XML: @[package:]color/filename
> - ColorStateList

```
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android" >
    <item
        android:color="hex_color"
        android:state_pressed=["true" | "false"]		//clicked, touched
        android:state_focused=["true" | "false"]		//useless
        android:state_selected=["true" | "false"]		//tab selected
        android:state_checkable=["true" | "false"]		//checkable non-checkable widget
        android:state_checked=["true" | "false"]		//checkable widget checked
        android:state_enabled=["true" | "false"]
        android:state_window_focused=["true" | "false"] />
</selector>

<Button
	android:textColor="@color/filename">
```




# [Drawable](https://developer.android.google.cn/guide/topics/resources/drawable-resource.html)
> - getDrawable(R.drawable.id)

#### BitmapDrawable
> - store at res/drawable/ .png | .jpg | .gif
> - store at res/drawable/filename.xml
> - ref in Java: R.drawable.filename
> - ref in XML:  @[package:]drawable/filename

> - png file or xml

```
<?xml version="1.0" encoding="utf-8"?>
<bitmap
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:src="@[package:]drawable/drawable_resource"
    android:antialias=["true" | "false"]
    android:dither=["true" | "false"]
    android:filter=["true" | "false"]
    android:gravity=["top" | "bottom" | "left" | "right" | "center_vertical" |
                      "fill_vertical" | "center_horizontal" | "fill_horizontal" |
                      "center" | "fill" | "clip_vertical" | "clip_horizontal"]
    android:mipMap=["true" | "false"]
    android:tileMode=["disabled" | "clamp" | "repeat" | "mirror"] />
```



> - use BitmapDrawable

```
<ImageView
    android:layout_height="wrap_content"
    android:layout_width="wrap_content"
    android:src="@drawable/myimage" />
```






#### NinePatchDrawable
> - store at res/drawable/filename.9.png
> - ref In Java：R.drawable.filename
> - ref In XML：@[package:]drawable/filename






#### LayerDrawable

```
<?xml version="1.0" encoding="utf-8"?>
<layer-list
    xmlns:android="http://schemas.android.com/apk/res/android" >
    <item
        android:drawable="@[package:]drawable/drawable_resource"
        android:id="@[+][package:]id/resource_name"
        android:top="dimension"
        android:right="dimension"
        android:bottom="dimension"
        android:left="dimension" />
    <item />
    <item />
</layer-list>
```









#### StateListDrawable

```
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_pressed="true"
          android:drawable="@drawable/button_pressed" /> <!-- pressed -->
    <item android:state_focused="true"
          android:drawable="@drawable/button_focused" /> <!-- focused -->
    <item android:state_hovered="true"
          android:drawable="@drawable/button_focused" /> <!-- hovered -->
    <item android:drawable="@drawable/button_normal" /> <!-- default -->
</selector>
```











#### LevelListDrawable















#### TransitionDrawable










#### InsertDrawable








#### ClipDrawable

```
<?xml version="1.0" encoding="utf-8"?>
<clip
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:drawable="@drawable/drawable_resource"
    android:clipOrientation=["horizontal" | "vertical"]
    android:gravity=["top" | "bottom" | "left" | "right" | "center_vertical" |
                     "fill_vertical" | "center_horizontal" | "fill_horizontal" |
                     "center" | "fill" | "clip_vertical" | "clip_horizontal"] />


<ImageView
    android:id="@+id/image"
    android:background="@drawable/clip"
    android:layout_height="wrap_content"
    android:layout_width="wrap_content" />



ImageView imageview = (ImageView) findViewById(R.id.image);
ClipDrawable drawable = (ClipDrawable) imageview.getDrawable();
drawable.setLevel(drawable.getLevel() + 1000);
```














#### ScaleDrawable














#### ShapeDrawable

```
<?xml version="1.0" encoding="utf-8"?>
<shape
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape=["rectangle" | "oval" | "line" | "ring"] >
    <corners
        android:radius="integer"
        android:topLeftRadius="integer"
        android:topRightRadius="integer"
        android:bottomLeftRadius="integer"
        android:bottomRightRadius="integer" />
    <gradient
        android:angle="integer"
        android:centerX="float"
        android:centerY="float"
        android:centerColor="integer"
        android:endColor="color"
        android:gradientRadius="integer"
        android:startColor="color"
        android:type=["linear" | "radial" | "sweep"]
        android:useLevel=["true" | "false"] />
    <padding
        android:left="integer"
        android:top="integer"
        android:right="integer"
        android:bottom="integer" />
    <size
        android:width="integer"
        android:height="integer" />
    <solid
        android:color="color" />
    <stroke
        android:width="integer"
        android:color="color"
        android:dashWidth="integer"
        android:dashGap="integer" />
</shape>
```



















#### AnimationDrawable

```
<animation-list android:id="@+id/selected" android:oneshot="false">
    <item android:drawable="@drawable/wheel0" android:duration="50" />
    <item android:drawable="@drawable/wheel1" android:duration="50" />
    <item android:drawable="@drawable/wheel2" android:duration="50" />
    <item android:drawable="@drawable/wheel3" android:duration="50" />
    <item android:drawable="@drawable/wheel4" android:duration="50" />
    <item android:drawable="@drawable/wheel5" android:duration="50" />
 </animation-list>
 ```













# [Layout](https://developer.android.google.cn/guide/topics/resources/layout-resource.html)
> - store at res/layout/filename.xml
> - ref In Java: R.layout.filename
> - ref In XML: @[package:]layout/filename


```
layout_width
layout_height                fill_parent【填充剩余】，wrap_content或者固定的像素值
                    
layout_marginLeft            
layout_marginTop             
layout_marginRight           
layout_marginBottom          边界

layout_gravity              在父元素中的停靠
gravity                     子组件的停靠,多个属性用竖线隔开
                            top、buttom、left、right、center、fill
                            center_vertical、fill_vertical、center_horizontal、fill_horizontal
                            clip_vertical、clip_horizontal

LinearLayout
    android:orientation     子组件的排列方式,horizontal|vertical(default)
    layout_weight        所有子View排布之后的剩余空间按照它们的layout_weight分配
                        fill_parent:weight越大view越小
                        wrap_content:weight越大view越大，前提是保证wrap_content

RelativeLayout
    android:layout_centerHorizontal     子组件是否在容器中水平居中 true|false
    android:layout_centerVertical       子组件是否在容器中垂直居中 true|false
    android:layout_centerInParent       子组件是否卫浴容器中央    true|false
    android:layout_alignParentBottom    是否与容器底部对齐       true|false 
    android:layout_alignParentLeft
    android:layout_alignParentRight
    android:layout_alignParentTop

    android:layout_above            本组件在某组件的上方
    android:layout_alignBaseline    本组件和某组件的基线对齐。
    android:layout_alignBottom      本组件的下边缘和某组件的的下边缘对齐
    android:layout_alignEnd         本组件的末端和某组件末端对齐
    android:layout_alignRight       本组件的右边缘和某组件的的右边缘对齐
    android:layout_alignLeft        本组件左边缘和某组件左边缘对齐
    android:layout_alignStart       本组件的开始端和某组件开始端对齐
    android:layout_alignTop         本组件的顶部和某组件的的顶部对齐
    android:layout_below            本组件在某组件的下方
     
    android:layout_toEndOf          本组件在某组件末端
    android:layout_toLeftOf         本组件在某组件的左边
    android:layout_toRightOf        本组件在某组件的右边
    android:layout_alignLeft        本组件在某组件开始端

FrameLayout
    android:foreground           前景图像
    android:foregroundGravity    前景图像的gravity属性

    先定义的位于底层，后定义的位于上层



//layout布局的属性
以下取值为:true|false
    android:layout_centerHrizontal      水平居中
    android:layout_centerVertical       垂直居中
    android:layout_centerInparent       相对于父元素完全居中

    android:layout_alignParentBottom        贴紧父元素的下边缘
    android:layout_alignParentLeft          贴紧父元素的左边缘
    android:layout_alignParentRight         贴紧父元素的右边缘
    android:layout_alignParentTop           贴紧父元素的上边缘
    android:layout_alignWithParentIfMissing 如果对应的兄弟元素找不到的话就以父元素做参照物


以下取值为id
    android:layout_below        在某元素的下方
    android:layout_above        在某元素的上方
    android:layout_toLeftOf     在某元素的左方
    android:layout_toRightOf    在某元素的右方

    android:layout_alignTop 与某元素的上边缘对齐
    android:layout_alignLeft    与某元素的左边缘对齐
    android:layout_alignBottom  与某元素的下边缘对齐
    android:layout_alignRight   与某元素的右边缘对齐
```


























# [Menu](https://developer.android.google.cn/guide/topics/resources/menu-resource.html)




























# [String](https://developer.android.google.cn/guide/topics/resources/string-resource.html)

```
<string name="welcome_messages">Hello, %1$s! You have %2$d new messages.</string>
Resources res = getResources();
String text = String.format(res.getString(R.string.welcome_messages), username, mailCount);


//Spannable

```


























# [Style](https://developer.android.google.cn/guide/topics/resources/style-resource.html)
> - store at res/values/filename.xml
> - ref In XML: @[package:]style/style_name

> - 在layout中设置style, 子view中不会继承属性
> - android.R.attr中有All style properties, 其中，window开头的属性仅支持Theme
> - android.R.styleable.Theme可以用于Theme中的标准属性
> - android.support.v7.appcompat.R.style
> - android.R.style所有style和theme
> - 其中，Theme_NoTitleBar=@android:style/Theme.NoTitleBar
> - 系统预定义Theme:
> - @android:style/Theme.Dialog
> - @android:style/Theme.Translucent










# [Misc](https://developer.android.google.cn/guide/topics/resources/more-resources.html)


