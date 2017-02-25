---
layout:     post
title:      "Android Components"
subtitle:   " \"Android Component\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - Android
---
><small>目录:[Android目录](/2014/06/09/android-index)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>

# Intent

#### usage

android.content.Context ctx

| ----------- | ------------------------------------------------------------------------------------- |
|to Activity  | ctx.startActvity(intent)                                                              |
|to Service   | ctx.startService(intent)<br>bindService(intent)<br>始终使用显式Intent                                      |
|to Broadcasts| ctx.sendBroadcasts()<br>sendOrderedBroadcasts(intent)<br>sendStickyBroadcasts(intent) |

> - 显式Intent

```
Intent downloadIntent = new Intent(this, DownloadService.class);
startService(downloadIntent);
```

> - 隐式Intent

```
Intent sendIntent = new Intent();
sendIntent.setAction(Intent.ACTION_SEND);
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
sendIntent.setType("text/plain");


//force to use application chooser
Intent chooser = Intent.createChooser(intent, "title");

// Verify the original intent will resolve to at least one activity
if (intent.resolveActivity(getPackageManager()) != null) {
    startActivity(chooser);
    
    //start activity without a chooser
    //if have more then one reciver activity, chooser will popup
    //if set one reciever acitivity, chooser will not popup
    //startActivity(sendIntent);
}



<activity android:name="ShareActivity">
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:mimeType="text/plain"/>
    </intent-filter>
</activity>
```




#### Pending Intent
> - wrapper for intent

> - NotificationManager 
> - Widget
> - AlarmManager

#### [Common Intent](https://developer.android.google.cn/guide/components/intents-common.html)


#### resolve Intent

> - action test
> - intent action is one of filter's  listed action
> - if filter has no action, not intent will pass
> - intent has no action, if filter has at least one action, pass


> - category test
> - test as category
> - default category is must for filter, as Android auto attach default category to implicated intent


> - data test
> - <data android:mimeType="video/*" android:scheme="..." android:host="" ... />
> - URI: <scheme>://<host>:<port>/<path>
> - URI example: content://com.example.project:200/folder/subfolder/etc

> - if filter has no scheme, ignore host
> - if filter has no host, ignore port
> - if filter has no scheme and host, ignore path

> - if filter only has scheme, test scheme only
> - if filter only has scheme & host, test scheme & host only
> - if filter only has scheme & host & path, test scheme & host & path only


> - if intent has no mimeType & URI, and filter has no mimeType & URI, pass
> - if intent has no mimeType but URI, and filter has no mimeType but URI, if URI match, pass
> - if intent has no URI but mimeType, and filter has no URI but mimeType, if mimeType match, pass
> - if filter only has mimeType, content: & file& scheme is included in this filter by default




#### action

```
setAction(String)

registerReceiver(BroadcastReceiver, IntentFilter) or a <receiver> tag in a manifest)
```


#### category

```
intent.addCategory(String)
intent.removeCategory(String)
```


#### extra

```
putExtra(String name, Parcelable value)
putExtra(String name, Parcelable[] value)

putExtra(String name, double value)
putExtra(String name, double[] value)

putExtra(String name, CharSequence value)
putExtra(String name, CharSequence[] value)

putExtra(String name, boolean value)
putExtra(String name, boolean[] value)

putExtra(String name, char value)
putExtra(String name, char[] value)

putExtra(String name, byte value)
putExtra(String name, byte[] value)

putExtra(String name, float value)
putExtra(String name, float[] value)

putExtra(String name, int value)
putExtra(String name, int[] value)


putExtra(String name, String value)
putExtra(String name, String[] value)

putExtra(String name, long value)
putExtra(String name, long[] value)


putExtra(String name, short[] value)
putExtra(String name, short value)

putExtra(String name, Bundle value)
putExtra(String name, Serializable value)
putExtras(Intent src)
putExtras(Bundle extras)


removeExtra(String name)
replaceExtras(Intent src)
replaceExtras(Bundle extras)



Bundle getExtras()
getLongExtra(String key)
getDoubleExtra(String key)
getFloatArrayExtra(String name)
getFloatExtra(String name, float defaultValue)
getIntExtra(String name, int defaultValue)
```

#### data

```
Uri uri =  Uri.parse("file://com.android.test:520/mnt/sdcard");
intent.setData(uri)
intent.setType(String mimeType); //Set an explicit MIME data type

```

  



















# Activity

#### life cycle

![life cycle](https://developer.android.google.cn/images/activity_lifecycle.png)

| -------------------- | ------------------------------- |
| onCreate             | being created                   |
| onStart              | ui loaded,visiable              |
| onResume             | interactable                    |
| onPause              | lose focus, still visable       | 
| onStop               | unvisiable, in background       |
| onDestroy            | about to be destroyed           |


![state](https://developer.android.google.cn/images/fundamentals/restore_instance.png)

> - onPause:save instance state here, for example: unsaved db record |
> - onSaveInstanceState: before activity killed，called before onPause()，保存临时状态，无法保证会调用
> - onRestoreInstanceState:保存一些在对ondestroy和oncreate方法的多次调用中需要保持的数据
> - onConfigrationChanged:
> - onNewIntent:
> - 屏幕方向、键盘可用性及语言等变化会引起onDestroy, onCreate


#### background translucent

```
//styles.xml
<style name="AppTheme.translucent" parent="AppTheme">
        <item name="android:windowBackground">@color/translucent_background</item>
    <item name="android:windowIsTranslucent">true</item>
</style>

//colors.xml
<color name="translucent_background">#60000000</color>
```

#### fullscreen

```
onCreate() {
  requestWindowFeature(Window.FEATURE_NO_TITLE);
  getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);
  super.onCreate()
}
```


#### customize TitleBar

```
//set layout
getWindow().setFeatureInt(Window.FEATURE_CUSTOM_TITLE, R.layout.custom_title_1);
requestWindowFeature(Window.FEATURE_LEFT_ICON);

//set left icon
getWindow().setFeatureDrawableResource(Window.FEATURE_LEFT_ICON,  android.R.drawable.ic_dialog_alert);

getWindow().setTitle("This is just a test”);
```



#### show as Dialog

```
<activity android:theme="@style/Theme.CustomDialog">
<style name="Theme.CustomDialog" parent="android:style/Theme.Dialog">
  <item name="android:windowBackground">@drawable/filled_box</item>
</style>
```

#### start for result

```
Intent intent = new Intent(ReceiveResult.this, SendResult.class);
startActivityForResult(intent, int GET_CODE);

void onActivityResult(int requestCode, int resultCode, Intent data) {
  //是从SendResult返回的
  if (requestCode == GET_CODE) 
  //返回的结果代码
  if (resultCode == Activity.RESULT_OK)
  //返回的Intent
  data.getAction();
}


//SendResult.java
setResult(RESULT_OK, (new Intent()).setAction("Corky!"));
finish();
```


#### configuration changes

```
onConfigrationChanged

```










# Framgment

#### Life Cycle

> - since 3.0, api 11
> - when activity stop, fragment stop
> - when activity destroyed, framgment destroyed
> - when activity running, add/remove fragment
> - put fragment change to activity stack

![Life Cycle](https://developer.android.google.cn/images/fragment_lifecycle.png)

| ----------------- | ----------------------------- |
| onCreate          | fragment being created        |
| onCreateView      | first time draw ui            |
| onPause           |
| onActivityCreated | after activity onCreate       |
| onDestoryView     |
| onAttach          |
| onDetach          |




#### Type
- DialogFragment
- ListFragment
- PreferenceFragment

#### Create

```
MyDialogFragment extends DialogFragment{
  @Override
  public Dialog onCreate(Bundle savedInstanceState) ｛
    int title = getArguments().getInt("title"); //deal with arguments
  }

  @Override
  public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    return inflater.inflate(R.layout.frag_mydialog, container, false);
  }
}

//1. the new 
MyDialogFragment mydialog = new MyDialogFragment();
Bundle args = new Bundle();
args.putInt("title", title);
mydialog.setArguments(args);
mydialog.show(getSupportFragmentManager(), "mydialog");


//2. the FragmentTransaction way
FragmentTransaction ft = getSupportFragmentManager().beginTransaction();
MyFragment f = Fragment.instantiate(context,  MyFragment.getName(),  args);
MyFragment f = new MyFragment();
ft.add(containerID, f);
ft.commit();
```


#### add to activity

```
//layout.xml
<framgment android:name="com.example.news.ArticleListFragment" android:id="@+id/" />


//FragmentTransaction
FragmentTransaction ft = getSupportFragmentManager().beginTransaction();
ft.add(containerId, fragment)
ft.replace(itemId, fragment)
//add fragment without ui, use tag
ft.add(fragment, tag);
ft.commit();
```

#### find fragment

```
//by id
MyFragment fragment = (ExampleFragment) getFragmentManager().findFragmentById(R.id.example_fragment);
//by tag
dialogFragment.show(ft, "tag");
Fragment prev = getFragmentManager().findFragmentByTag("tag");
```



#### FragmentTransaction

```
FragmentTransaction ft = getSupportFragmentManager().beginTransaction();

ft.add(fragment, tag);
ft.add(containerId, fragment);
ft.findFragmentById(id);
ft.popBackStack();

ft.addToBackStack(null);
ft.attach(fragment);
ft.detach(fragment);
ft.show(fragment);
ft.hide(fragment);
ft.remove(fragment);
ft.replace(itemId, fragment);
ft.setCustomeAnimations(enter, exit);
ft.Transition(transit);
ft.setTransitionStyle(styleID);
ft.commit();
```



#### communicate with Activity

```
//fragment get reference of a view in activity
View listView = getActivity().findViewById(R.id.list);

//activity get reference of a framgment
ExampleFragment fragment = (ExampleFragment) getFragmentManager().findFragmentById(R.id.example_fragment);
```



# Activity Stack

> - 系统同时存在多个Task
> - 不同应用的Activity放在同一个Task堆栈中
> - Activity全部弹出，Task结束
> - Home使当前Task移到后台
> - [TODO](https://developer.android.google.cn/guide/components/tasks-and-back-stack.html#ManagingTasks)










# Service

> - service do not start a thread, can assigned to run a specific thread

#### Life Cycle

```
//if service is not running
//startService, bindService both start this service
//when service started, it call onCreate()
onCreate()
onDestory

//run on foregroud, for example: Music Service
startForeground
stopForeground
```

#### start 

```
context.startService()
//start service, context exit, service still running
//untile call context.stopService() or service.stopSelf()

service.onStartCommand
//process request from context



context.bindService()
//bind context to service, allow user interact
//can bind saveral context to a same service
//when no context bind to this service, service exit

service.onBind
//process request from context

context.unbind
```

#### connection

```
ServiceConnection connection = new ServiceConnection(){
  public void onServiceConnected(ComponentName name, IBinder binder){}
  public void onServiceDisconnected(ComponentName name) {}
};

bindService(new Intent(context, LocalService.class), connection, Context.BIND_AUTO_CREATE);
unbindService(connection);
```

#### IntntService

IntentService use worker-thread<br>
onHanadleInput(Intent intent):process request<br>
use queue<br>
after queue finished, IntentService call stopSelf()<br>






# Content Provider
ContentResolver借用URI来找到ContentProvider应用程序，并进行CRUD

Uri uri = Uri.parse("content://com.wang.myprovider")
Uri sub = Uri.parse("content://com.wang.myprovider/users")

class MyContentProvider extends ContentProvider {
  query
  insert
  update
  delete
  getType
  onCreate
}


以表的形式组织所有数据
在app之间共享数据

content://com.example.transportationprovider/trains/122
A:标准前缀
B:URI标识
C:path
D:id


UriMatcher
UriMatcher  sMatcher = new UriMatcher(UriMatcher.NO_MATCH);
sMatcher.addURI("com.bing.procvide.personprovider", "person", 1);

ContentUris
Uri uri = Uri.parse("content://com.bing.provider.personprovider/person")
Uri resultUri = ContentUris.withAppendedId(uri, 10); 
long personid = ContentUris.parseId(resultUri);//获取的结果为:10





android.content.ContentProvider.ContentProvider

boolean onCreate
Uri insert(Uri uri, ContentValues values)
int delete(Uri uri, String selection, String[] selectionArgs)
int update(Uri uri, ContentValues values, String selection, String[] selectionArgs)
Cursor query(Uri uri, String[] projection, String selection, String[] selectionArgs, String sortOrder)

String getType(Uri uri)


集合类型
MIME类型字符串应该以vnd.android.cursor.dir/开头
非集合类型
MIME类型字符串应该以vnd.android.cursor.item/开头


ContentResolver
ContentResolver resolver =  activity.getContentResolver();
Uri uri = Uri.parse("content://com.bing.provider.personprovider/person");

//value pairs
ContentValues values = new ContentValues();
values.put("name", "bingxin");
values.put("age", 25);
resolver.insert(uri, values); 

resolver.query
resolver.update
resolver.delete


//listen to value change in ContentProvider




# App Widgets

```
//AndroidManifest.xml
<application>
  <receiver android:name="AppWidget">
    <intent-filter>
      <action android:name="android.appwidget.action.APPWIDGET_UPDATE"></action>
    </intent-filter>
    <meta-data android:name="android.appwidget.provider" android:resource="@xml/widget_info" />
  </receiver>
</application>
```

```
//res/xml.widget_info.xml
<?xml version="1.0" encoding="utf-8"?>
<appwidget-provider
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:minWidth = "294dp"
    android:minHeight = "72dp"
    android:updatePeriodMillis = "86400000"
    android:initialLayout = "@layout/appwidgetlayout"
    >
</appwidget-provider>
```

```
//layout/appwidgetlayout.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android" android:layout_width="fill_parent" android:layout_height="fill_parent">
  <TextView 
    android:id="@+id/txtapp" 
    android:text="test" 
    android:layout_width="wrap_content" 
    android:layout_height="wrap_content" 
    android:background="#ffffff"></TextView>
  <Button 
    android:id="@+id/btnSend" 
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" 
    android:text="Send"></Button>
</LinearLayout>
```

```
public class AppWidget extends AppWidgetProvider {
  onDeleted //删除一个AppWidget时调用
  onDisabled//最后一个appWidget被删除时调用
  onEnabled //AppWidget的实例第一次被创建时调用
  onReceive //接受广播事件
  onUpdate  //到达指定的更新时间或者当用户向桌面添加AppWidget时被调用
}


public void onUpdate(Context context, AppWidgetManager appWidgetManager, int[] appWidgetIds)
{
  Intent intent = new Intent();
  intent.setAction(broadCastString);
 
  //设置pendingIntent的作用
  PendingIntent pendingIntent = PendingIntent.getBroadcast(context, 0, intent, 0);
  RemoteViews remoteViews  = new RemoteViews(context.getPackageName(),R.layout.appwidgetlayout);
        
 
  //绑定事件
  remoteViews.setOnClickPendingIntent(R.id.btnSend, pendingIntent);
         
  //更新Appwidget
  appWidgetManager.updateAppWidget(appWidgetIds, remoteViews);
}

public void onReceive(Context context, Intent intent)
{
  if (intent.getAction().equals(broadCastString))
  {               
    //只能通过远程对象来设置appwidget中的控件状态
    RemoteViews remoteViews  = new RemoteViews(context.getPackageName(),R.layout.appwidgetlayout);
 
    //通过远程对象将按钮的文字设置为”hihi”
    remoteViews.setTextViewText(R.id.btnSend, "hihi");   
            
    //获得appwidget管理实例，用于管理appwidget以便进行更新操作
    AppWidgetManager appWidgetManager = AppWidgetManager.getInstance(context);
           
    //相当于获得所有本程序创建的appwidget
    ComponentName componentName = new ComponentName(context,AppWidget.class);
           
    //更新appwidget
    appWidgetManager.updateAppWidget(componentName, remoteViews);
  }
  super.onReceive(context, intent);
}

```

# Processes&Threads

```
//work thread
public void onClick(View v) {
  new Thread(new Runnable() {
    public void run() {
      final Bitmap bitmap = loadImageFromNetwork(“http://example.com/image.png");
      //在非UI线程中，不能直接改变UI属性
      mImageView.post(new Runnable() {
        public void run() {
          mImageView.setImageBitmap(bitmap);
        }
      });
    }
  }).start();
}
```

```
//Using AsyncTask
public void onClick(View v) {
    new DownloadImageTask().execute("http://example.com/image.png");
}

//<传入参数，onProgressUpdate参数，onPostExecute参数>
private class DownloadImageTask extends AsyncTask<String, Void, Bitmap> {
  /** The system calls this to perform work in a worker thread and
   * delivers it the parameters given to AsyncTask.execute() */
  protected Bitmap doInBackground(String... urls) {
    return loadImageFromNetwork(urls[0]);
  }
    
  /** The system calls this to perform work in the UI thread and delivers
   * the result from doInBackground() */
  protected void onPostExecute(Bitmap result) {
    mImageView.setImageBitmap(result);
  }
}
```


