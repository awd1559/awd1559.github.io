---
layout:     post
title:      "Android-Universal-Image-Loader"
subtitle:   " \"Load image\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
><small>[Android-Universal-Image-Loader](https://github.com/nostra13/Android-Universal-Image-Loader)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>


# install

```
compile 'com.nostra13.universalimageloader:universal-image-loader:1.9.5'
```

```
<manifest>  
  <!-- load image from internet -->
  <uses-permission android:name="android.permission.INTERNET" />
  <!-- cache images on SD card -->
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
</manifest>
```

```
@Override 
void onCreate(Bundle savedInstanceState) {
  //config and initialize ImageLoader
  ImageLoaderConfiguration config = new ImageLoaderConfiguration.Builder(this).build();
  ImageLoader.getInstance().init(config);
}
```

	