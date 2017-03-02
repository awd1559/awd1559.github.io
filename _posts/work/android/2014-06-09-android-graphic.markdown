---
layout:     post
title:      "Android Graphic"
subtitle:   " \"Android Graphic\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - Android
---
><small>目录:[Android目录](/2014/06/09/android)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>


```
private class myview extends View{
    public myview(Context context) {
        super(context);
    }
    protected void onDraw(Canvas canvas){
        canvas.drawColor(Color.BLACK);

        Paint paint = new Paint();
        paint.setColor(Color.RED);
        paint.setTextSize(30);
        canvas.drawText("save:begin", 0, 100, paint);
        
        canvas.save();
        canvas.translate(200, 200);
        canvas.rotate(-10);
        paint.setColor(Color.BLUE);
        canvas.drawRect(0, 0, 200, 200, paint);
        canvas.clipRect(0, 0 , 200, 200);
        paint.setColor(Color.GREEN);
        canvas.drawText("in save text", 0, 0, paint);
        canvas.restore();
        
        canvas.drawText("resore:end", 0, 150, paint);
    }
}
```

