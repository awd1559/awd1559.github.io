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


# Font

```
//assert font
mText.setTypeface(Typeface.createFromAsset(getAssets(),"fonts/HandmadeTypewriter.ttf"));
```



# OpenGL

```
GLActivity extends Activity{
    mGLSurfaceView = new GLSurfaceView(this);
    mGLSurfaceView.setRenderer(new CubeRenderer(false));
    setContentView(mGLSurfaceView);
}

class CubeRenderer implements Renderer{
    onDrawFrame{
        gl.glClearColor(0, 0, 0, 0);
        gl.glClear(GL10.GL_COLOR_BUFFER_BIT | GL10.GL_DEPTH_BUFFER_BIT);
        
        draw();
    }
    onSurfaceChanged
    onSurfaceCreated
}
```




# draw view

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




# Surface

```
MyView extends SurfaceView implements SurfaceHolder.Callback{

    public void surfaceCreated(SurfaceHolder holder, int format, int width, int height){}
    public void surfaceChanged(SurfaceHolder holder){}
    
    public MyView(){
        getHolder().addCallback(this);
    }
    
    
    Canvas canvas = this.surfaceHolder.lockCanvas(null);
    //draw
    this.surfaceHolder.unlockCanvasAndPost(canvas);
}
```


> - GLSurfaceView

```
class MyGLSurfaceView extends GLSurfaceView{
    public MyGLSurfaceView(Context context){
        MyRenderer myRenderer = new MyRenderer();
        setRenderer(myRenderer);
        setRenderMode(GLSurfaceView.RENDERMODE_CONTINUOUSLY);
        
    }
}

class MyRenderer implements GLSurfaceView.Renderer{
    public void onDrawFrame(GL10 gl){       //绘图
        gl.glClear
        gl.glVertexPointer
        gl.glColorPointer
        gl.glDrawArrays
    }
    
    public void onSurfaceChanged(GL10 gl, int width, int height){
        gl.glViewport
        gl.glLoadIdentity
        gl.glFrustumf
    }
    public void onSurfaceCreated(GL10 gl, EGLConfig config) {//创建时被调用
        gl.glDisable(GL10.GL_DITHER);//关闭抗抖动           
        gl.glEnable(GL10.GL_DEPTH_TEST);//启用深度测试
    }
}
```



```
//在SurfaceView上画图
SurfaceHolder surfaceholder = surfaceview.getHolder();
Canvas canvas = surfaceholder.lockCanvas(null);
 ......
surfaceholder.unlockCanvasAndPost(canvas);

//在surfaceView上播放视频
mediaPlayer.setDisplay(surfaceholder);
mediaPlayer.setDataSource(path);
mediaPlayer.prepare();
mediaPlayer.start();

//在surfaceView上预览Camera
android.hardware.Camera
Camera camera = Camera.open();
camera.setPreviewDisplay(surfaceholder);
camera.startPreview();
```




# image
> - 错误消息：
> - bitmap size exceeds VM budget
> - 应该是图片占用的内存超过了系统虚拟机可分配的最大限制
> - 不同手机可能分配的最大值不一样
> - 后来找到解决办法主要是设置BitmapFactory.Options

```
BitmapFactory.Options bitmapOptions = new BitmapFactory.Options();
bitmapOptions.inSampleSize = 4;
bitmap = BitmapFactory.decodeStream(this.getContentResolver()..openInputStream(uri), null , bitmapOptions);

//获取bitmap的方法
//使用res.drawable
BitmapDrawable bmpDraw=(BitmapDrawable)res.getDrawable(R.drawable.pic180);
Bitmap bmp=bmpDraw.getBitmap();

//使用磁盘图片
File f=new File(fileName); 
Bitmap bmp = BitmapFactory.decodeFile(fileName);
mImageView.setImageBitmap(bmp);

//从stream中
InputStream is = context.getResources().openRawResource(R.drawable.app_sample_code);
mBitmap = BitmapFactory.decodeStream(is);

// 转换为BitmapDrawable对象
BitmapDrawable bmpDraw=new BitmapDrawable(bmp);

//在view中显示位图
ImageView iv2 = (ImageView)findViewById(R.id.ImageView02);
iv2.setImageDrawable(bmpDraw);
//使用ID
ImageView.setImageResource(R.drawable.imageid);

//Canvas类的drawBirmap()显示位图


//Metrics放大缩小图片
DisplayMetrics dm=new DisplayMetrics();
getWindowManager().getDefaultDisplay().getMetrics(dm);
displayWidth=dm.widthPixels;
displayHight=dm.heightPixels;
Bitmap mySourceBmp = BitmapFactory.decodeResource(getResources(), R.drawable.hippo);


Matrix matrix = new Matrix();  
matrix.postScale(scaleWidth, scaleHeight); 
Bitmap resizeBmp = Bitmap.createBitmap(bmp,0,0,bmpWidth,bmpHeight,matrix,true); 

//旋转
matrix.setRotate(5*ScaleAngle);


//从一张图中截取
Bitmap.createBitmap(bitmap, x, y, width, height);
```















