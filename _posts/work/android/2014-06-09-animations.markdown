---
layout:     post
title:      "Android Animation"
subtitle:   " \"Android Animation\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
category: android
permalink: /android/animations
tags:
    - Android
---
><small>目录:[Android目录](/android/)</small>




# PropertyAnimation

```
android.animation.Animator
    android.animation.ValueAnimator
        android.animation.TimeAnimator
        android.animation.ObjectAnimator
    android.animation.AnimatorSet
```

#### ValueAnimator
> - since api 11
> - a time engine, not really change the property of object

```
TextView textView;

ValueAnimator animator = ValueAnimator.ofInt(0,200);
animator.setDuration(300);
animator.setRepeatCount(3);
animator.setRepeatMode(ValueAnimator.REVERSE);
animator.setTarget(textView);
animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
    @Override
    public void onAnimationUpdate(ValueAnimator valueAnimator) {
        int animatorValue = (int)valueAnimator.getAnimatedValue();
        textView.setX(animatorValue);
    }
});
animator.start();
```

```
PropertyValuesHolder xproperty = PropertyValuesHolder.ofInt("x", 0, 300);
PropertyValuesHolder yproperty = PropertyValuesHolder.ofInt("y", 0, 300);
ValueAnimator animator = ValueAnimator.ofPropertyValuesHolder(xproperty, yproperty);
animator.setDuration(300);
animator.setRepeatCount(3);
animator.setRepeatMode(ValueAnimator.REVERSE);
animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
    @Override
    public void onAnimationUpdate(ValueAnimator valueAnimator) {
        int animatorValueX =  (int) valueAnimator.getAnimatedValue("x");
        int animatorValueY = (int) valueAnimator.getAnimatedValue("y");

        textView.setX(animatorValueX);
        textView.setY(animatorValueY);
    }
});
animator.start();
```




#### ObjectAnimator
> - since api 11

```
ObjectAnimator alpha = ObjectAnimator.ofFloat(textView, "alpha", 0f, 1f);
alpha.setDuration(2000);//设置动画时间
alpha.setInterpolator(new DecelerateInterpolator());//设置动画插入器，减速
alpha.setRepeatCount(-1);//设置动画重复次数，这里-1代表无限
alpha.setRepeatMode(ObjectAnimator.REVERSE);//设置动画循环模式。
alpha.start();//启动动画。
```



animator.clone()
animator.reverse()

animator.setDuration(1500)
animator.setCurrentPlayTime(seekTime) //0 ~ 1500

animator.addListener(new Animator.AnimatorListener() {});
animator.addUpdateListener(ValueAnimator.AnimatorUpdateListener() {});



#### AnimatorSet
> - since api 11

```
AnimatorSet bouncer = new AnimatorSet();
bouncer.play(colorAnim).before(squashAnim1);
bouncer.play(squashAnim1).with(squashAnim2);   //with是同时播放
bouncer.play(bounceBackAnim).after(stretchAnim2);
```




# ViewAnimation

```
android.view.animation.Animation
    android.view.animation.AlphaAnimation
    android.view.animation.RotateAnimation
    android.view.animation.ScaleAnimation
    android.view.animation.TranslateAnimation
    android.view.animation.AnimationSet
```


```
Animation animation = AnimationUtils.loadAnimation(MainActivity.this, R.anim.push);
image.startAnimation(animation);

//使用代码
animation = new AlphaAnimation(float from, float to);
animation = new RotateAnimation(fromDegree, toDegree);
animation = new ScaleAnimatioin(xFrom, xTo, yFrom, yTo);
animation = new TranslateAnimation(xFrom, xTo, yFrom, yTo);
animation = new AnimationUtils.loadAnimation(context, R.anim.shak);

animation.setDuration(500);
animation.setStartOffset(300);
animation.setRepeatMode(Animation.RESTART);
animation.setRepeatCount(Animation.INFINITE);
animation.setInterpolator(new AccelerateInterpolator(float factor));
animation.setInterpolator(AnimationUtils.loadInterpolator(this, android.R.anim.accelerate_interpolator));

//开始动画
someview.startAnimation(animation);




///Interpolator
///LinearInterpolator   线性变化
///AccelerateInterpolator   加速变化
///DecelerateInterpolator   减速效果
R.anim.filename.xml         @anim/filename
<overshootInterpolator xmlns:android="http://schemas.android.com/apk/res/android"
    android:tension="7.0" />

<set android:interpolator="@anim/filename"> //set interpolator
    ...
</set>

/////Android predefined Interpolators
AccelerateDecelerateInterpolator        @android:anim/accelerate_decelerate_interpolator
AccelerateInterpolator              @android:anim/accelerate_interpolator
AnticipateInterpolator              @android:anim/anticipate_interpolator
AnticipateOvershootInterpolator     @android:anim/anticipate_overshoot_interpolator
BounceInterpolator              @android:anim/bounce_interpolator
CycleInterpolator               @android:anim/cycle_interpolator
DecelerateInterpolator          @android:anim/decelerate_interpolator
LinearInterpolator              @android:anim/linear_interpolator
OvershootInterpolator               @android:anim/overshoot_interpolator



//AnimationSet
AnimationSet set = new AnimationSet(false);
set.addAnimation(anim);
```
