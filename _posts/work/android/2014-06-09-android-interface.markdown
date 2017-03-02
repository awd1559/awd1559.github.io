---
layout:     post
title:      "Android User Interface"
subtitle:   " \"Android UserInterface\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - Android
---
><small>目录:[Android目录](/2014/06/09/android)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>


# Layout

#### LinearLayout

#### RelativeLayout

#### ListView

> - 从raw/txt 中获取内容

```
private ArrayList<String> loadItems(int rawResourceId) {
    try {
        ArrayList<String> countries = new ArrayList<String>();
        InputStream inputStream = getResources().openRawResource(rawResourceId);
        BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
        String line;
        while ((line = reader.readLine()) != null) {
            countries.add(line);
        }
        reader.close();
        return countries;
    } catch (IOException e) {
        return null;
    }
}

ArrayList<String> items = loadItems(R.raw.sites);
ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, items);
listView.setAdapter(adapter);
```






> - ExpandableList
> - ExpandableListActivity
> - ExpandableListAdapter adapter = new MyExpandableListAdapter();
> - setListAdapter(adapter);

```
<ExpandableListView 
    android:id="@+id/list"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:background="#ffffff"
    android:cacheColorHint="#00000000"
    android:listSelector="#00000000" />

class MyExpandableListAdapter extends BaseExpandableListAdapter {
    private String[] groups = {"1", "2", "3", "4"};
    private String[][] children = {
        {},
        {}
    };
    TextView getTextView(){
        AbsListView.LayoutParams lp = new AbsListView.LayoutParams(ViewGroup.LayoutParams.FILL_PARENT, 64);
        TextView textView = new TextView(ExpandableListActivity.this);
        textView.setLayoutParams(lp);
        textView.setGravity(Gravity.CENTER_VERTICAL);
        textView.setPadding(36, 0, 0, 0);
        textView.setTextSize(20);
        textView.setTextColor(Color.BLACK);
        return textView;
    }
    
    @Override
    public int getGroupCount() {
        return groups.length;
    }
    
    @Override
    public long getGroupId(int groupPosition){
        return groupPosition;
    }
    
    @Override
    public Object getGroup(int groupPosition) {
        return groups[groupPosition];
    }
    
    @Override
    public int getChildrenCount(int groupPosition) {
        return children[groupPosition].length;
    }
    
    @Override
    public long getChildId(int groupPosition, int childPosition) {
        return childPosition;
    }
    
    @Override
    public Object getChild(int groupPosition, int childPosition) {
        return children[groupPosition][childPosition];
    }
    
    @Override
    public boolean hasStableIds() {
        return true;
    }
    
    @Override
    public boolean isChildSelectable(int groupPosition, int childPosition){
        return true;
    }
    
    @Override
    public View getGroupView(int groupPosition, boolean isExpanded, View convertView, ViewGroup parent) {
        LinearLayout ll = new LinearLayout(ExpandableListActivity.this);
        ll.setOrientation(LinearLayout.HORIZONTAL);
        TextView textView = getTextView();
        textView.setTextColor(Color.BLACK);
        textView.setText(getGroup(groupPosition).toString());
        ll.addView(textView);
        
        return ll;
    }
    
    @Override
    public View getChildView(int groupPosition, int childPosition, boolean isLastChild, View convertView, ViewGroup parent) {
        LinearLayout ll = new LinearLayout(ExpandableListActivity.this);
        ll.setOrientation(LinearLayout.HORIZONTAL);
        TextView textView = getTextView();
        textView.setTextColor(Color.RED);
        textView.setText(getChild(groupPosition, childPosition).toString());
        ll.addView(textView);
        return ll;
    }
}
```





> - 事件
> - ListView响应点击和长按事件

```
listView.setOnItemClickListener(new android.widget.AdapterView.OnItemClickListener() {
    @Override
    public void onItemClick(AdapterView<?> parent, View view, int position,long id) {
        Map<String, Object> map = (Map<String, Object>)parent.getItemAtPosition(position);
        Intent intent = (Intent) map.get("intent");
        startActivity(intent);
    }   
});
```



```
adapter.notifyDataSetChanged                //刷新listview
listview.smoothScrollToPosition(0);                 //移动到首部
listview.smoothScrollToPosition(listView.getCount() - 1)
```




> - 继承自ListActivity
> -     1)可直接setAdapter
> -     2)如果除ListView外，还包括其他的View
> -     3)layout中必须有<ListView android:id="@android:id/list" />
      
> - 使用Activity, ListAdapter
> - 方法1：ArrayAdapter

```
//最简单的ArrayAdapter使用String数组
String[] data =     {"1", "2", "3", "4", "5"};
ListView listView = (ListView)findViewById(R.id.mylist);
ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, data);
listview.setAdapter(adapter);
```


> - 方法2：SimpleAdapter

```
//SimpleAdapter:使用List<HashMap>
List<Map<String, Object>> data = new ArrayList<Map<String, Object>>();
Map<String, Object> temp = new HashMap<String, Object>();
temp.put("title", name);
temp.put("intent", intent);
data.add(temp);
SimpleAdapter adapter = new SimpleAdapter(this, data, 
    android.R.layout.simple_list_item_1,
    new String[] { "title" },
    new int[] { android.R.id.text1 });
```


> - 方法3：SimpleCursorAdapter

```
//使用Cursor数据指针adapter
Cursor c = getContentResolver().query(People.CONTENT_URI, null, null, null, null);
startManagingCursor(c);
ListAdapter adapter = new SimpleCursorAdapter(this, 
    android.R.layout.simple_list_item_1, c,
    new String[] {People.NAME},
    new int[] {android.R.id.text1});
```





> - 方法4：extends ArrayAdapter

```
class TestAdapter extends ArrayAdapter<String>{
    private LayoutInflater layouter;
    private int layoutId;

    public TestAdapter(Context context, int resource, int textViewResourceId) {
        super(context, resource, textViewResourceId);
        this.layoutId = resource;
        layouter = LayoutInflater.from(Android_test_adapterActivity.this);
    }       
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View view = layouter.inflate(layoutId, null);           //从xml中来
        TextView title = (TextView) view.findViewById(R.id.title);
        TextView params = (TextView) view.findViewById(R.id.params);
        String string = getItem(position);
        String[] arr = string.split(";");
        title.setText(arr[0]);
        if (arr.length == 2) {
            params.setText(arr[1]);
        } else {
            params.setVisibility(View.GONE);
        }
        return view;
    }
}
```



> - 方法5：extends BaseAdapter

```
class MyImgAdapter extends BaseAdapter{
    private Context context;
        
    public MyImgAdapter(Context context){
        super();
        this.context = context;
    }
        
    private int[] imgs = {R.drawable., R.drawable.};
    @Override
    public int getCount() {return imgs.length;}
    @Override
    public Object getItem(int position) {return position;}
    @Override
    public long getItemId(int position) {return position;}
        
    public View getView(int position, View convertView, ViewGroup parent) {
           ImageView iv = new ImageView(context);
        iv.setImageResource(imgs[position]);
        iv.setLayoutParams(new ListView.LayoutParams(80, 80));
        iv.setScaleType(ImageView.ScaleType.FIT_XY);

        return iv;
     }
}
```





















#### GridView









# ViewGroup




#### ViewFlipper
> - 自动切换view

```
<ViewFlipper>
    <view1 />
    <view2 />
    <view3 />
    <view4 />
</ViewFlipper>

ViewFlipper flipper = findViewById;
flipper.addView(view, ViewGroup.LayoutParams);
flipper.setFlipInterval(2000);
flipper.startFlipping();        
//或者
filpper.showNext();
```

> - Gesture

```
//in onCreate
GestureDetector detector = new GestureDetector(this, new PageFlipOnGestureListener(this));

public boolean onTouchEvent(MotionEvent event) {
    return this.detector.onTouchEvent(event);
}


//OnGestureListener
class PageFlipOnGestureListener implements GestureDetector.OnGestureListener {
    private Context myContext;

    public PageFlipOnGestureListener(Context context) {
        myContext = context;
    }

    @Override
    public boolean onFling(MotionEvent e1, MotionEvent e2, float velocityX, float velocityY) {
        if (e1.getX() - e2.getX() > 120) {// 如果是从右向左滑动
            // 注册flipper的进出效果
            myflipper.setInAnimation(AnimationUtils.loadAnimation(myContext, R.anim.right_in));
            myflipper.setOutAnimation(AnimationUtils.loadAnimation(myContext, R.anim.left_out));
            myflipper.showNext();
            return true;
        } else if (e1.getX() - e2.getX() < -120) {// 如果是从左向右滑动
            myflipper.setInAnimation(AnimationUtils.loadAnimation(myContext, R.anim.left_in));
            myflipper.setOutAnimation(AnimationUtils.loadAnimation(myContext, R.anim.right_out));
            myflipper.showPrevious();
            return true;
        }
        return false;
    }

    @Override public boolean onDown(MotionEvent e) {return false;}
    @Override public void onLongPress(MotionEvent e) {}
    @Override public boolean onScroll(MotionEvent e1, MotionEvent e2, float distanceX, float distanceY){return false;}
    @Override public void onShowPress(MotionEvent e) {}
    @Override public boolean onSingleTapUp(MotionEvent e) { return false; }
}

//animation
//res/anim/left_in.xml
<translate xmlns:android="http://schemas.android.com/apk/res/android" 
    android:fromXDelta="-100%p" android:toXDelta="0" android:duration="500" />
//res/anim/left_out.xml
<translate xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromXDelta="0" android:toXDelta="-100%p" android:duration="500" />
//right_in.xml
<translate xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromXDelta="100%p" android:toXDelta="0" android:duration="500" />
//right_out.xml
<translate xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromXDelta="0" android:toXDelta="100%p" android:duration="500" />
```


> - ViewPager

```
<android.support.v4.view.ViewPager
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <android.support.v4.view.PagerTitleStrip
    <android.support.v4.view.PagerTabStrip
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_gravity="top" />
</android.support.v4.view.ViewPager>


LayoutInflater inflater = getLayoutInflater();  
view1 = inflater.inflate(R.layout.layout1, null);  
view2 = inflater.inflate(R.layout.layout2, null);  
view3 = inflater.inflate(R.layout.layout3, null);  

viewList = new ArrayList<View>();// 将要分页显示的View装入数组中  
viewList.add(view1);  
viewList.add(view2);  
viewList.add(view3);  

titleList = new ArrayList<String>();// 每个页面的Title数据  
titleList.add("title_1");  
titleList.add("title_2");  
titleList.add("title_3");  

PagerAdapter mPagerAdapter = new PagerAdapter() {
    @Override
    public Object instantiateItem(ViewGroup container, int position) {
        ((ViewPager)container).addView(viewList.get(position));
        return position;
    }

    @Override
    public void destroyItem(ViewGroup container, int position, Object object) {
        container.removeView(viewList.get(position));
    }

    @Override
    public boolean isViewFromObject(View view, Object object) {
        return view == viewList.get((int)Integer.parseInt(object.toString()));
    }

    @Override
    public int getCount() {
        return viewList.size();
    }

    @Override
    public CharSequence getPageTitle(int position) {
        return titleList.get(position);
    }
};

ViewPager mypager = (ViewPager)findViewById(R.id.pager);
mypager.setAdapter(mPagerAdapter);
```

> - user FragmentPagerAdapter
> - use PagerTabStrip




#### SlidingDrawer
> - since api 3
> - Deprecated since api 17

```
<SlidingDrawer
    android:id="@+id/drawer"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:handle="@+id/handle"
    android:content="@+id/content">
    <ImageView
      android:id="@id/handle"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:src="@drawable/tray_handle_normal"
    />
    <Button
      android:id="@id/content"
      android:layout_width="fill_parent"
      android:layout_height="fill_parent"
      android:text="I'm in here!"
    />
</SlidingDrawer>




<SlidingDrawer  android:handle="@+id/iv" 
        android:content="@+id/myContent" 
        android:orientation="vertical">
<ImageView
        android:id="@+id/iv" />
<GridView 
      android:id="@id/myContent" />
</SlidingDrawer>
SlidingDrawer sd = (SlidingDrawer)findViewById(R.id.sd);
ImageView iv=(ImageView)findViewById(R.id.iv);
sd.setOnDrawerOpenListener(new SlidingDrawer.OnDrawerOpenListener(){
    @Override
    public void onDrawerOpened() {
        iv.setImageResource(R.drawable.close1);//响应开抽屉事件 ，把图片设为向下的
    }
});

sd.setOnDrawerCloseListener(new SlidingDrawer.OnDrawerCloseListener() {
    @Override
    public void onDrawerClosed(){
        iv.setImageResource(R.drawable.open1);//响应关抽屉事件
    }
});
```







#### ViewSwitcher

#### ImageSwitcher

#### TextSwitcher




#### spinner
> - dropdown menu 

```
<Spinner
    android:entries="@array/colors"
    android:prompt="string"
/>
```



```
adapter = new ArrayAdapter<String>(this,
    android.R.layout.simple_spinner_item, countriesStr);
adapter.setDropDownViewResource(R.layout.myspinner_dropdown);   //设置下拉菜单的显示方式
spinner.setAdapter(adapter);
spinner.setOnItemSelectedListener(new Spinner.OnItemSelectedListener() {
  @Override
  public void onItemSelected(AdapterView<?> arg0, View arg1, int arg2,
      long arg3)
  {
    myTextView.setText("ll" + countriesStr[arg2]);
    arg0.setVisibility(View.VISIBLE);
  }

  @Override
  public void onNothingSelected(AdapterView<?> arg0)
  {
    // TODO Auto-generated method stub
  }

});
```


#### Gallery
> - deprecated in api 16

```
<ImageSwitcher android:id="@+id/switcher"
    android:layout_width="320dp"
    android:layout_height=“320dp" />
<Gallery android:id="@+id/gallery"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="25dp" 
    android:unselectedAlpha="0.6"
    android:spacing=“3pt" />    

Gallery gallery = (Gallery) findViewById(R.id.gallery);
ImageSwitcher switcher = (ImageSwitcher) findViewById(R.id.switcher);
switcher.setFactory(new ViewFactory()
{
    @Override
    public View makeView()
    {
        ImageView imageView = new ImageView(GallaryTest.this);
        imageView.setBackgroundColor(0xff0000);
        imageView.setScaleType(ImageView.ScaleType.FIT_CENTER);
        imageView.setLayoutParams(new ImageSwitcher.LayoutParams(
        LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT));
        return imageView;
    }
});
// 设置图片更换的动画效果
switcher.setInAnimation(AnimationUtils.loadAnimation(this, android.R.anim.fade_in));
switcher.setOutAnimation(AnimationUtils.loadAnimation(this, android.R.anim.fade_out));

// 创建一个BaseAdapter对象，该对象负责提供Gallery所显示的图片
BaseAdapter adapter = new BaseAdapter()
{
    @Override
    public int getCount()
    {
        return imageIds.length;
    }
    @Override
    public Object getItem(int position)
    {
        return position;
    }
    @Override
    public long getItemId(int position)
    {
        return position;
    }
    // 该方法的返回的View就是代表了每个列表项
    @Override
    public View getView(int position, View convertView, ViewGroup parent)
    {
        // 创建一个ImageView
        ImageView imageView = new ImageView(GallaryTest.this);
        imageView.setImageResource(imageIds[position % imageIds.length]);
        // 设置ImageView的缩放类型
        imageView.setScaleType(ImageView.ScaleType.FIT_XY);
        imageView.setLayoutParams(new Gallery.LayoutParams(75, 100));
        TypedArray typedArray = obtainStyledAttributes(R.styleable.Gallery);
    imageView.setBackgroundResource(typedArray.getResourceId(R.styleable.Gallery_android_galleryItemBackground, 0));
        return imageView;
    }
};
    gallery.setAdapter(adapter);
    gallery.setOnItemSelectedListener(new OnItemSelectedListener()
    {
        // 当Gallery选中项发生改变时触发该方法
        @Override
        public void onItemSelected(AdapterView<?> parent, View view, int position, long id)
        {
            switcher.setImageResource(imageIds[position % imageIds.length]);
        }
        @Override
        public void onNothingSelected(AdapterView<?> parent)
        {}
});
//res/values/attr.xml
<declare-styleable name="Gallery">
        <attr name="android:galleryItemBackground" />
</declare-styleable>
```




# Popup

#### PopupWindow
> - popup不是模态窗口，弹出后仍然可以访问activity中的控件。


```
LayoutInflater inflater = LayoutInflater.from(getApplicationContext());
View view = inflater.inflate(R.layout.popupwindow, null);
mPopupWindow = new PopupWindow(view, 400, ViewGroup.LayoutParams.WRAP_CONTENT);
mPopupWindow.setBackgroundDrawable(getResources().getDrawable(R.drawable.bg_frame));  

mPopupWindow.setTouchable(true);  
mPopupWindow.setFocusable(true);
//只有touchable=true,focusable=false时才起作用
mPopupWindow.setOutsideTouchable(true);
 
mPopupWindow.update(); 
mPopupWindow.showAtLocation(view, Gravity.CENTER, 0, 0); 


//使用系统动画  
mPopupWindow.setAnimationStyle(R.style.PopupAnimation); 
<style name="PopupAnimation" parent="android:Animation"
        mce_bogus="1">
        <item name="android:windowEnterAnimation">@anim/popup_show</item>
        <item name="android:windowExitAnimation">@anim/popup_dismis</item>
</style>


//anim/popup_show.xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <scale android:fromXScale="0.6" android:toXScale="1.1"
        android:fromYScale="0.6" android:toYScale="1.1" android:pivotX="50%"
        android:pivotY="50%" android:duration="200" />
    <scale android:fromXScale="1.0" android:toXScale="0.91"
        android:fromYScale="1.0" android:toYScale="0.91" android:pivotX="50%"
        android:pivotY="50%" android:duration="400" android:delay="200" />
    <alpha android:interpolator="@android:anim/linear_interpolator"
        android:fromAlpha="0.0" android:toAlpha="1.0" android:duration="400" />
</set>

//anim/popup_dismis.xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <scale android:fromXScale="1.0" android:toXScale="1.25"
        android:fromYScale="1.0" android:toYScale="1.25" android:pivotX="50%"
        android:pivotY="50%" android:duration="200" />
    <scale android:fromXScale="1.0" android:toXScale="0.48"
        android:fromYScale="1.0" android:toYScale="0.48" android:pivotX="50%"
        android:pivotY="50%" android:duration="400" android:delay="200" />
    <alpha android:interpolator="@android:anim/linear_interpolator"
        android:fromAlpha="1.0" android:toAlpha="0.0" android:duration="400" />
</set>
```


#### PopupMenu

```
PopupMenu popup = new PopupMenu(this, view);
popup.getMenuInflater().inflate(R.menu.popup, popup.getMenu());

popup.setOnMenuItemClickListener(new PopupMenu.OnMenuItemClickListener() {
    public boolean onMenuItemClick(MenuItem item) {
        Toast.makeText(MyActivity.this, "Clicked popup menu item " + item.getTitle(),Toast.LENGTH_SHORT).show();
        return true;
    }
});

popup.show();
```


# Input Controls

#### Button

#### TextField

```
<TextView 
    android:lines="2"
    android:ems="12"
    android:autoLink="web|email"
/>
```

> - 设置字体

```
Typeface type = Typeface.create(Typeface.SERIF, Tapeface.ITALIC);
Typeface type = Typeface.createFromAsset(getContext().getAssets(), "fonts/chess.ttf");
tv.setTypeface(type);
```

> - Html样式

```
String textStr1 = "<font color=\"#ffff00\">如果有一天，</font><br>";
tv.setText(Html.fromHtml(textStr1));


Spanned text = Html.fromHtml(source);
tv.setText(text);
```


> - 粗体

```
android:textStyle="bold"                    //设置粗体
tv.getPaint().setFakeBoldText(true);        //设置中文粗体
```


> - 文字中插入图片

```
String imgStr = "<img src=\""+R.drawable.sidai+"\"/>";
Html.ImageGetter imageGetter = new Html.ImageGetter() {
    public Drawable getDrawable(String url) {
       int id =Integer.parseInt(url);
       Drawable draw =getResources().getDrawable(id);
       draw.setBounds(10, 10, 228,300);
       return draw;
    }
};
tv.append(Html.fromHtml(imgStr,imageGetter,null));
第二种方法是使用xml布局文件中一系列android:drawableXXX

<2>
android:drawableBottom="@drawable/xxxx"
```

> - 隐藏输入法：

```
EditText et=(EditText)findViewById(R.id.name);
et.setInputType(InputType.TYPE_DATETIME_VARIATION_NORMAL);
    
//在xml中可以使用属性，但不实用：
<EditText android:id="@+id/name" android:windowSoftInputMode="stateAlwaysHidden" />


TextPaint paint = view.getPaint();
paint.setShadowLayer()

Layout.getDesiredWidth(String textPaint);
```


> - 改变drawable的显示level

```
ClipDrawable drawable = (ClipDrawable) imageview.getBackground();
drawable.setLevel(3000);
```



```
TextView
    android:autoLink            是否转为可点击超链接
    none|web|email|phone|map|all

    android:cursorVisible       文本框的光标
    android:drawableBottom      底端绘制制定图像
    android:drawableLeft        
    android:drawableRight
    android:drawableTop
    android:drawablePadding     文本与绘制图像之间的间距
    android:edittable           文本是否可编辑
    android:ellipsize           文本超过TextView长度如何处理
        none:不进行处理
        start:省略开头部分
        middle:省略中间部分
        end:省略结尾
        marquee:
    android:gravity             文本对齐方式
    android:height              文本高度(以pixel为单位)
    android:hint                内容为空时，默认显示的提示文本
    android:minHeight           
    android:maxHeight
    android:minWidth
    android:maxWidth
    android:lines               内容行数
    android:MinLines            内容最少行数
    android:MaxLines            内容最多行数
    android:password            以点代替字符
    android:phoneNumber         只接受电话号码
    android:scrollHorizontally         如果不够现实，是否可水平滚动
    android:selectAllOnFocus    如果内容可选，获得焦点时选中所有文本
    android:singleLine      true，则单行模式，不换行
    android:shadowColor     阴影颜色
    android:shadowDx        阴影水平偏移
    android:shadowDy        阴影垂直偏移
    android:shadowRadius    阴影角度
    android:text
    android:textColor           内容颜色
    android:textColorHighlight  内容选中时颜色
    android:textScaleX          内容在水平方向上的缩放因子
    android:textSize      
    android:textStyle           字体风格，如粗体、斜体
    android:typeface            设置字体
    android:width               文本框宽度(以pixel为单位)
```










> - EditText中文字自动变成链接

```
<TextView
    android:autoLink="web|phone|email"
/>

        final EditText txtLinkify = (EditText) findViewById(R.id.txtLinkify);
        txtLinkify.setOnKeyListener(new View.OnKeyListener() {
            
            @Override
            public boolean onKey(View v, int keyCode, KeyEvent event) {
                Linkify.addLinks(txtLinkify, Linkify.EMAIL_ADDRESSES|
                        Linkify.WEB_URLS|
                        Linkify.PHONE_NUMBERS);
                return false;
            }
        });
```







#### EditText

```
<EditText
    android:singleLine="true"
    android:lines="4"
    android:hint="type here"
    android:selectAllOnFocus="true"    //点击自动选中所有文字
/>







editText.setFilters(new InputFilter[] {
    new InputFilter.AllCaps(),
    new InputFilter.LengthFilter(2)
});
```






#### Checkbox


> - checkbox自定义

```
checkBox.setOnClickListener(new View.OnClickListener(){
    public void onClick(View v){
        checkBox.isChecked()
    }
});
```

```
<CheckBox
    android:button=“@drawable/checkable"/>

//res/drawable/checkable.xml
<selector>
   <item android:state_enabled="true" android:state_checked="true" android:drawable="@drawable/reg_ischeck" />
    <item android:drawable="@drawable/reg_nocheck" />
</selector>
```




#### RadioButton

```
<RadioGroup
    <RadioButton android:id="" android:text="" />
    <RaidoButton android:id="" android:text="" 
    android:button=“@null”
    />
/>

radioGroup.setOnCheckedChangeListener(new RadioGroup.onCheckedChangeListener(){
    public void onCheckedChanged(RadioGroup group, int checkedId){
        if(checkedId != -1)
        RadioButton rb = (RadioButton) findViewById(checkedId);
        radioGropuu.clearCheck();
    }
});
```




#### ToggleButton

```
<ToggleButton
    android:text="Toggle"
    android:textOff="Disabled"
    android:textOn="Enabled"
/>
```






#### Picker

```
final DatePicker date = (DatePicker)findViewById(R.id.DatePicker0);
date.init(date.getYear(), date.getMonth(), date.getDayOfMonth(), new DatePicker.onDateChangedListener(){
    public void onDateChanged(DatePicker view, int year, int monthOfYear, int dayOfMonth){
        Date dt = new Date(year-1990, monthOfyear, dayOfMont, time.getCurrentHour(), time.getCurrentMinute());
        text.setText(dt.toString());
    }
});


time.setOnTimeChangedListener(new TimePicker.onTimeChangedListener(){
    public void onTimeChanged(TimePicker view, int hourOfDay, int minute){
        Date dt = new Date(date.getYear()-1990, date.getMonth(), date.geDayOfMonth(), hourOfDay, minute);
    }
});
```


#### ProgressBar

```
<ProgressBar
    style="?android:attr/progressBarStyleHorizontal"
    android:max="100"
/>
progressBar.setProgress(75);

//在页面加载前放置progressbar,放在right side of the title bar
requestWindowFeature(Window.FEATURE_INDETERMINATE_PROGRESS);
requestWindowFeature(Widnow.FEATURE_PREOGRESS);
setContentView(R.layout.indicators);
setProgressBarIndeterminateVisibility(true);
setProgressBarVisibility(true);
setPregress(500);




//自定义旋转ProgressBar
<ProgressBar
    style="?android:attr/progressBarStyle"  
    android:indeterminateDrawable="@drawable/progress_my_style" />
//drawable/progress_my_style.xml
<animated-rotate xmlns:android="http://schemas.android.com/apk/res/android" 
    android:drawable="@drawable/audio_player_03"
    android:pivotX="50%"
    android:pivotY="50%"
/>



android:progressDrawable="@drawable/barbg" 
//res/drawable/barbg.xml
<layer-list xmlns:android="http://schemas.android.com/apk/res/android" >
    <!-- 背景图 -->
    <item
        android:id="@+android:id/background"
        android:drawable="@drawable/bar_empty"/>
    <!-- 第二进度图,可以不用 -->
    <item
        android:id="@+android:id/SecondaryProgress"
        android:drawable="@drawable/bar_empty"/>
    <!-- 进度度，填充图 -->
    <item
        android:id="@+android:id/progress"
        android:drawable="@drawable/bar_fill"/>
</layer-list>




//横条ProgressBar
<ProgressBar
    style="?android:attr/progressBarStyleHorizontal"
    android:progressDrawable="@drawable/progressbarstyle" />
//drawable/progressbarstyle.xml
<?xml version="1.0" encoding="UTF-8"?>  
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">  
        <item android:id="@android:id/background" android:drawable="@drawable/bg" />  
        <item android:id="@android:id/secondaryProgress" android:drawable="@drawable/secondary" />  
        <item android:id="@android:id/progress" android:drawable="@drawable/progress" />  
</layer-list>
```


#### RatingBar

```
<RatingBar
    android:numSarts="4"
    android:stepSize="0.25" />


rate.setOnRatingBarChangeListener(new RatingBar.OnRatingBarChangeListener(){
    public void onRatingChanged(RatingBar ratingBar, flaot rating, boolean fromTouch){}
});

```



#### SeekBar


> - Event

```
seek.setOnSeekBarChangeListener(new SeekBar.onSeekBarChangeListener(){
    public void onProgressChanged(SeekBar seekBar, int progress, boolean fromTouch){
        seekBar.setSecondaryProgress( (progress+seekBar.getMax())/2 );
    }
});
```







> - 自定义

```
<SeekBar
    android:progressDrawable="@xml/progress_drawable"
    android:thumb="@xml/thumb_drawable" />
//xml/progress_drawable.xml
<?xml version="1.0" encoding="UTF-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="line">
    <stroke android:width="2dp" android:color="#ff585858"/>
</shape>
//xml/thumb_drawable.xml
<?xml version="1.0" encoding="UTF-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <gradient android:startColor="#ffffffff" android:endColor="#ff585858" android:angle="270"/>
    <size android:height="20dp" android:width="20dp"/>
</shape>
```







> - 自定义

```
<SeekBar
        android:id="@+id/seekBar1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:progressDrawable="@drawable/seekbar_bg"   
        android:thumb="@drawable/thumb_bar"            
        android:layout_alignParentLeft="true"
        android:layout_centerVertical="true" />

//res/drawable/seekbar_bg.xml
<layer-list xmlns:android="http://schemas.android.com/apk/res/android" >
    <!-- 背景图,空图 -->
    <item
        android:id="@+android:id/background"
        android:drawable="@drawable/bar_empty"/>
    <!-- 第二进度图 ， 可以不用—>
    <item
        android:id="@+android:id/SecondaryProgress"
        android:drawable="@drawable/bar_empty"/>
    <!-- 进度度 ，填充图 -->
    <item
        android:id="@+android:id/progress"
        android:drawable="@drawable/bar_full"/>
</layer-list>
//或者不用图片，用颜色
<item
        android:id="@+android:id/progress">
        <clip>
            <shape>
                <corners android:radius="5dip" />
                <gradient
                    android:angle="270"
                    android:endColor="#008000"
                    android:startColor="#33FF33" />
            </shape>
        </clip>
    </item>
//res/drawable/thumb_bar.xml

//seekbar上的把手图
<selector xmlns:android="http://schemas.android.com/apk/res/android" >
    <!-- 按下状态 -->
    <item android:state_pressed="true"
        android:drawable="@drawable/bar_thumb" />
    <!-- 焦点状态 -->
    <item android:state_focused="true"
        android:drawable="@drawable/bar_thumb" />
    <!-- 默认状态 -->
    <item android:drawable="@drawable/bar_thumb_dn" /> 

</selector>
```


#### ImageView

```
android:scaleType           图片如何resized/moved来匹配Imageview的size
    CENTER/center           按图片原来的size居中显示，截取图片的居中部分显示
    CENTER_CROP/centerCrop      按比例扩大图片的size居中显示
    CENTER_INSIDE/centerInside  按比例缩小图片的size居中显示
    FIT_CENTER/fitCenter        按比例扩大/缩小
    FIT_END/fitEnd          显示在view的下部
    FIT_START/fitStart      显示在view的上部
    FIT_XY/fitXY            扩大/缩小到view的大小显示
    MATRIX/matrix       动态

```


#### Chronometer

```
计时器<Chronometer  android:format="Timer: %s" />
```

















# ActionBar
> - since api 11, included in support v7
> - use ToolBar, DONOT use ActionBar

# ToolBar
> - since api 21, inlcuded in support v7
> - android.support.v7.widget.ToolBar
> - android.support.v4.widget.DrawerLayout


```
compile 'com.android.support:appcompat-v7:newestVersion'
compile 'com.android.support:design:newestVersion'
compile 'com.android.support:support-v4:newestVersion'
```



> - activity_main.xml

```
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    tools:openDrawer="start">

    <LinearLayout
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <android.support.design.widget.AppBarLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

            <android.support.v7.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:background="?attr/colorPrimary"
                android:minHeight="?attr/actionBarSize"
                android:theme="@style/Toolbar"
                app:popupTheme="@style/ThemeOverlay.AppCompat.Light" />

        </android.support.design.widget.AppBarLayout>


        <android.support.design.widget.CoordinatorLayout
            android:id="@+id/coordinatorLayout"
            android:background="@android:color/white"
            android:layout_width="match_parent"
            android:layout_height="match_parent">



            <FrameLayout
                android:background="@android:color/white"
                android:id="@+id/contentFrame"
                android:layout_width="match_parent"
                android:layout_height="match_parent"/>

            <android.support.design.widget.FloatingActionButton
                android:id="@+id/fab_add_task"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_margin="@dimen/fab_margin"
                android:src="@drawable/ic_add"
                app:fabSize="normal"
                app:layout_anchor="@id/contentFrame"
                app:layout_anchorGravity="bottom|right|end" />
        </android.support.design.widget.CoordinatorLayout>
    </LinearLayout>


    <android.support.design.widget.NavigationView
        android:id="@+id/nav_view"
        android:layout_gravity="start"
        android:fitsSystemWindows="true"
        app:headerLayout="@layout/nav_header"
        app:menu="@menu/drawer_actions"
        android:layout_width="wrap_content"
        android:layout_height="match_parent" />

</android.support.v4.widget.DrawerLayout>
```


> - styles.xml
```
<resources>
    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>

    <style name="Toolbar" parent="ThemeOverlay.AppCompat.Dark.ActionBar" />
</resources>
```





```
private void init() {
    //setup the toolbar
    Toolbar toolbar = (Toolbar)findViewById(R.id.toolbar);
    setSupportActionBar(toolbar);
    ActionBar bar = getSupportActionBar();
    bar.setHomeAsUpIndicator(R.drawable.ic_menu);
    bar.setDisplayHomeAsUpEnabled(true);

    //setup the navigation menu
    mDrawerLayout = (DrawerLayout) findViewById(R.id.drawer_layout);
    mDrawerLayout.setStatusBarBackground(R.color.colorPrimaryDark);
    NavigationView navigationView = (NavigationView) findViewById(R.id.nav_view);
    if(navigationView != null) {
        setupDrawerContent(navigationView);
    }

    //setup the fragment
    MainFragment tasksFragment = (MainFragment) getSupportFragmentManager().findFragmentById(R.id.contentFrame);
    if (tasksFragment == null) {
        // Create the fragment
        tasksFragment = MainFragment.newInstance();
        FragmentTransaction transaction = getSupportFragmentManager().beginTransaction();
        transaction.add(R.id.contentFrame, tasksFragment);
        transaction.commit();
    }
}

//the home trigger MenuItem
@Override
public boolean onOptionsItemSelected(MenuItem item) {
    switch (item.getItemId()) {
        case android.R.id.home:
            // Open the navigation drawer when the home icon is selected from the toolbar.
            mDrawerLayout.openDrawer(GravityCompat.START);
            return true;
    }
    return super.onOptionsItemSelected(item);
}
```




> - Fragment

```
public class MainFragment extends Fragment {
    public MainFragment() {}

    public static MainFragment newInstance() {
        return new MainFragment();
    }

    @Override
    public View onCreateView(LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        View root = inflater.inflate(R.layout.tasks_frag, container, false);

        FloatingActionButton fab = (FloatingActionButton) getActivity().findViewById(R.id.fab_add_task);

        fab.setImageResource(R.drawable.ic_add);
        fab.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {}
        });
        
        setHasOptionsMenu(true);
        return root;
    }

    @Override
    public void onCreateOptionsMenu(Menu menu, MenuInflater inflater) {
        inflater.inflate(R.menu.tasks_fragment_menu, menu);
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        switch (item.getItemId()) {
            case R.id.menu_clear:
                break;
            case R.id.menu_filter:
                showFilteringPopUpMenu();
                break;
            case R.id.menu_refresh:
                break;
        }
        return true;
    }



    public void showFilteringPopUpMenu() {
        PopupMenu popup = new PopupMenu(getContext(), getActivity().findViewById(R.id.menu_filter));
        popup.getMenuInflater().inflate(R.menu.filter_tasks, popup.getMenu());

        popup.setOnMenuItemClickListener(new PopupMenu.OnMenuItemClickListener() {
            public boolean onMenuItemClick(MenuItem item) {
                switch (item.getItemId()) {
                    case R.id.active:
                        break;
                    case R.id.completed:
                        break;
                    default:
                        break;
                }
                return true;
            }
        });

        popup.show();
    }
}
```







# Settings
> - Preferences
> - use PreferenceActivity before api 11
> - use PreferenceFragment after api 11

```
Class MyPreferences extends PreferenceActivity
onCreate
    addPreferencesFromResouce(R.xml.mypreferences);
```



> - 自定义Preference方法

```
class MyPreference extends Preference {
    public MyPreference(Context context, AttributeSet attrs) {
            super(context, attrs);

            setWidgetLayoutResource(R.layout.preference_widget_mypreference);
    }

    @Override
    protected void onBindView(View view)
        super.onBindView(view);
        final View = (View) view.findViewById(R.id.id);
    }

    @Override
    protected void onClick(){
        persistInt(intValue);   //保存
        notifyChanged();
    }

    //可以从xml中读取defaultValue
    @Override
    protected Object onGetDefaultValue(TypedArray a, int index) {
            return a.getInteger(index, 0);
    }
}
```




> - set SharedPreferences
> - stored at data/dadta/package_name/shared_prefs/PREFERENCESNAME.xml
> - 运行一次PreferenceActivity之后，其中的value才能准确读取到

```
SharedPreferences setting = PreferenceManager.getDefaultSharedPreferences(context);
SharedPreferences setting = getSharedPreferences(PREFERENCESNAME, MODE_PRIVATE);    
setting.edit()
    .putString("name", txtMyname.getText().toString())
    .putString("value", txtMyvalue.getText().toString())
    .commit();

//get preference
SharedPreferences setting = PreferenceManager.getDefaultSharedPreferences(context);
String setting.getString("key", "defaultvalue");
Set<String> setting.getStringSet
```









# Dialog

```
activity.showDialog():    to display a Dialog,将会调用onCreateDialog()
activity.dismissDialog(): to stop showing a Dialog
activity.removeDialog():  to remove a Dialog from Activity object Dialog pool

onCreateDialog()  //返回Dialog
onPrepareDialog()


protected Dialog onCreateDialg(int id){
    return dailog;
}
```

> - simple Dialog

```
Dialog simpleDialog = new Dialog(this);
simpleDialog.setTitle("");
```

> - Alert Dialog

```
AlertDialog alertDialog = new AlertDialog.Builder(this);
    .setTitle("")
    .setMessage("")
    .create();

new AlertDialog.Builder(EX03_12.this)
    .setIcon(R.drawable.icon)
    .setTitle(R.string.app_about)
    .setMessage(R.string.app_about_msg)
    .setPositiveButton(R.string.str_ok,
         new DialogInterface.OnClickListener()
         {
           public void onClick(DialogInterface dialoginterface, int i)
           {
           }
         }
    )
    .setNegativeButton
    .setNeutralButton       //三个按钮
    
    .setItems(R.array.select_dialog_items,              //列表
        new DialogInterface.OnClickListener() { 
            public void onClick(DialogInterface dialog, int which) {

                String[] items = getResources().getStringArray(R.array.select_dialog_items);
                new AlertDialog.Builder(AlertDialogSamples.this)
                    .setMessage("You selected: " + which + " , " + items[which])
                    .show();
                }
        })
        
    .setSingleChoiceItems(R.array.select_dialog_items, new DialogInterface.OnClickListener(){}) //单选列表
    .setMultiChoiceItems(R.array.select_dialog_items, new DialogInterface.OnClickListener(){})  //多选列表
    .setMultiChoiceItems(cursor, new DialogInterface.OnClickListener(){})                       //多选列表
    
    .setView(view)                                      //定制的外观
    .create()
    .show();
```    
 
> - PrograssDialog

```
myProgressDialog = new ProgressDialog(EX03_18.this);
myProgressDialog.setIcon(R.drawable.icon)
                .setTitle(strDialogTitle)
                .setProgressStyle(ProgressDialog.STYLE_HORIZONTAL)
                .setMax()
                .setButton("ok", new DialogInterface.onClickListener(){})
                .setButton2()
                .show();
                    
myProgressDialog = ProgressDialog.show(EX03_18.this, strDialogTitle, strDialogBody, true);

new Thread()
{ 
    public void run()
    { 
        int Progress = 0;  
        while(Progress < MAX_PROGRESS) {  
        try {  
            Thread.sleep(100);  
            Progress++;    
            myProgressDialog.incrementProgressBy(1);  
        }
        catch (Exception e)
        {
            e.printStackTrace();
        }
        finally
        {
            //取消PrograssDialog
            myDialog.dismiss();
        }
    }
}.start();
```



> - Character Dialog

```
CharacterPickerDialog charDialog = new CharacterPickerDialog(this, new View(this), null, "aeiou1234", false) {
    public void onItemClick(AdapterView parent, View view,int position, long id) {}
    public void onClick(View v) {}
};
```


> - DatePickerDialog

```
Calendar c = Calendar.getInstance();
Dialog dialog = new DatePickerDialog(           //创建DatePickerDialog对象
                 this,
                 new DatePickerDialog.OnDateSetListener(){  //创建OnDateSetListener监听器
                    @Override
                    public void onDateSet(DatePicker dp, int year, int month,int dayOfMonth) {      
                        EditText et = (EditText)findViewById(R.id.et);
                        et.setText("您选择了："+year+"年"+month+"月"+dayOfMonth+"日");
                    }                    
                 },
                 c.get(Calendar.YEAR),                  //传入年份
                 c.get(Calendar.MONTH),                 //传入月份
                 c.get(Calendar.DAY_OF_MONTH)           //传入天数     
              );
```

> - TimePickerDialog

```
Dialog dialog = new TimePickerDialog(this, new TimePickerDialog.OnTimeSetListener(){
    @Override
    public void onTimeSet(TimePicker tp, int hourOfDay, int minute) {
        EditText et = (EditText)findViewById(R.id.et);
        et.setText("您选择了："+hourOfDay+"时"+minute+"分");       //设置EditText控件的属性
    }                    
 },
 c.get(Calendar.HOUR_OF_DAY),       //传入当前小时数
 c.get(Calendar.MINUTE),            //传入当前分钟数
 false
);
```






> - 定制Dialog

```
<activity android:theme="@android:style/Theme.Dialog"
      android:name="DialogActivity"

requestWindowFeature(Window.FEATURE_LEFT_ICON);
setContentView(R.layout.dialog_activity);
getWindow().setFeatureDrawableResource(Window.FEATURE_LEFT_ICON, android.R.drawable.ic_dialog_alert);
```




> - 自定义对话框
> - <1>继承自Dialog类
> - Oncreate方法中通过setContentView来设置视图布局

> - <2>修改系统dialog外观

```
<style name="Theme_dialog" parent="@android:style/Theme.Dialog">
    <item name="android:windowBackground">@android:color/transparent</item>
    <item name="android:windowNoTitle">true</item>
</style>
```











# Notification

```
NotificationManager nm = (NotificationManager)getSystemService(NOTIFICATION_SERVICE);
//点击notification跳转的Intent
PendingIntent contentIntent = PendingIntent.getActivity(this, 0, new Intent(this, IncomingMessageView.class), 0);                       
Notification notif = new Notification(R.drawable.stat_sample, tickerText, System.currentTimeMillis());
notif.setLatestEventInfo(this, “from”, “message”, contentIntent);
//0ms delay, 震动250ms, 暂停100ms, 震动500ms
notif.vibrate = new long[] { 0, 250, 100, 500};
nm.notify(R.string.imcoming_message_ticker_text, notif);

//取消
nm.cancel(id);
```

# Toast

```
Toast.makeText(context, “string”, Toast.LENGTH_SHORT).show();


//Toast使用自定义的View
Toast mToast = new Toast(context);
ImageView mView = new ImageView(this);

mView.setImageResource(R.drawable.icon);
toast.setDuration(Toast.LENGTH_LONG);
mToast.setView(mView);
mToast.show();
```





# Menu

```
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:support="http://schemas.android.com/apk/res-auto" >
    <item
        android:id="@+id/menu_refresh"
        android:icon="@drawable/ic_action_refresh"
        android:title="@string/menu_refresh"
        support:showAsAction="ifRoom"/>
    <item
        android:id="@+id/menu_settings"
        android:icon="@drawable/ic_action_settings"
        android:title="@string/menu_settings"
        support:showAsAction="never"/>
</menu>


//Menu on ToolBar
public boolean onCreateOptionsMenu(Menu menu){
    getMenuInflater().inflate(R.menu.menu, menu);

    MenuItem locationItem = menu.add(0, R.id.menu_location, 0, R.string.menu_location);
    locationItem.setIcon(R.drawable.ic_action_location);

    MenuItemCompat.setShowAsAction(locationItem, MenuItem.SHOW_AS_ACTION_IF_ROOM);
    return true;
}

//二层目录
public boolean onCreateOptionsMenu(Menu menu){
    super.onCreateOptionsMenu(menu);
    menu.add("Forms")
        .seticon(android.R.drawable.ic_menu_edit)
        .setIntent(new Intent(this, FormsActivity.class));

    SubMenu sub = menu.addSubMenu("Style");
    sub.add(style_group, dark_id, 2, "Dark")
       .setChecked(true);
    sub.setGroupCheckable(style_group, true, true);

    return true;
}

//menu项响应
public boolean onOptionsItemSelected(MenuItem item){
    if(item.getItemId() == dark_id){
        return true;    
    }
    return super.onOptionsItemSelected(item);
}


registerForContextMenu(timer);

//长按menu
public void onCreateContextMenu(ContextMenu menu, View v, ContextMenuInfo menuInfo){
    super.onCreateContextMenu(menu, v, menuInfo);

    if(v.getId() == R.id.Chro){
        getMenuInflater().inflate(R.menu.timer_context, menu);
        menu.setHeaderIcon(android.R.drawable.ic_media_play);
            .setHeaderTitle("Timer controls");
    }
}

//长按menu项响应 
public boolean onContextItemSelected(MenuItem item){
    super.onContextitemSelected(item);
}
```




# Search

```
<android.support.v7.widget.SearchView
        android:id="@+id/searchView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:iconifiedByDefault="false"
        android:queryHint="请输入搜索内容" />




SearchView mSearchView = (SearchView) findViewById(R.id.searchView);

// 设置搜索文本监听
mSearchView.setOnQueryTextListener(new SearchView.OnQueryTextListener() {
    // 当点击搜索按钮时触发该方法
    @Override
    public boolean onQueryTextSubmit(String query) {
        return false;
    }

    // 当搜索内容改变时触发该方法
    @Override
    public boolean onQueryTextChange(String newText) {
        if (!TextUtils.isEmpty(newText)){
            mListView.setFilterText(newText);
            tv.setText(newText);
        }else{
            mListView.clearTextFilter();
            tv.setText("hello");
        }
        return false;
    }
});



//设置suggestion
SearchView.OnSuggestionListener

mSearchView.setOnSuggestionListener(new SearchView.OnSuggestionListener() {
    @Override
    public boolean onSuggestionClick(int position) {

    }

    @Override
    public boolean onSuggestionSelect(int position) {

    }
});
```



> - create searchable activity

```
<activity android:name="SearchableActivity">
    <intent-filter>
        <action android:name="android.intent.action.SEARCH" />
    </intent-filter>
    <meta-data android:name="android.app.searchable" android:resource="@xml/searchable" />
</activity>

<meta-data android:name="android.app.default_searchable" android:value="SearchableActivity" />

//res/xml/searchable.xml
<?xml version="1.0" encoding="utf-8"?>
<searchable xmlns:android="http://schemas.android.com/apk/res/android"
    android:label="@string/app_name"
    android:hint="hint"
    android:icon="@mipmap/ic_launcher"
    android:searchMode="queryRewriteFromText" />
```



```
onSearchRequested(){    //开始搜索
    Bundle appData = new Bundle();
    appData.putBoolean(SearchableActivity.JARGON, true);
    startSearch(null, false, appData, false);
    return true;
}

Activity接收搜索框的搜索请求，获得参数
Bundle appData = getintent().getBundleExtra(SearchManager.APP_DATA);
if(appData != null){
    boolean jargon = appData.getBoolean(SearchableActivity.JARGON);
}

能搜索的Activity中开始SEARCH intent，再次生成一个该Activity
如果是android:launchMode="singleTop"
onNewIntent(Intent intent){
    setIntent(intent);
    handleIntent(intent);
}
```



















# Scroll

> - Scroller的使用

```
Scroller mScroller;
init(Context context){
    mGestureDetector = new GestureDetector(context, mGestureListener);
    mGestureDetector.setIsLongpressEnabled(false);
    mScroller = new Scroller(context, new DecelerateInterpolator());
}

@Override
public boolean onTouchEvent(MotionEvent event) {
    if(!mGestureDetector.onTouchEvent(event) && event.getAction() == MotionEvent.ACTION_UP){
    }
    return true;
}

onDraw(){
    canvas.save();
    canvas.translate(0, -mLastScrollY);
    staticlayout.draw(canvas);
    canvas.restore();
}

//or

@Override
public void computeScroll() {
    if(mScroller.computeScrollOffset()){//当动画没有停止时
        scrollTo(mScroller.getCurrX(), mScroller.getCurrY());//如果动画没有停止  那么一直更新子View的值
        postInvalidate();
    }
}
```

> - 在mGestureListener中处理所有的滚动事件

```
private SimpleOnGestureListener mGestureListener = new SimpleOnGestureListener() {
    public boolean onDown(MotionEvent event) {
        if (isScrolling) {
            mScroller.forceFinished(true);
            return true;
        }
        return false;
    }

    public boolean onScroll(MotionEvent e1, MotionEvent e2, float dx, float dy) {
        mScroller.startScroll(0, mLastScrollY, 0, (int) -dy, 400);
        mLastScrollY += dy;
            
        invalidate();
        return true;
    }

    public boolean onFling(MotionEvent e1, MotionEvent e2, float vx, float vy) {
        //int maxY = 0x7FFFFFFF;
        //int minY = -maxY;
        int maxY = mViewHeight * getChildCount();
        int minY = 0;
        mScroller.fling(0, mLastScrollY, 0, (int) -vy / 2, 0, 0, minY, maxY);   //mLastScrollY未处理
        invalidate();
        return true;
    }
};
```


> - ScrollView
> - 只能上下滚动，  左右滚动使用HorizontalScrollView
> - 只能有一个直接子view

```
android:scrollbars="vertical"   //显示是滚动条位置，可为none
android:scrollbarFadeDuration   //滚动条淡出效果时间
android:scrollbarStyle      //滚动条的风格和位置

android:scrollbarSize       //滚动条的宽度。           大小受限制
android:scrollbarThumbHorizontal    //水平滚动条的drawable。   必须为shape或nine-patch     
android:scrollbarThumbVertical      //垂直滚动条的drawable.       必须为shape或nine-patch     


scrollView.arrowScroll(View.FOCUS_DOWN);    //一次方向键按键
scrollView.pageScroll(View.FOCUS_DOWN);     //滚动一屏
scrollView.scroll(0, 0);            //
scrollView.smoothScrollTo(0, 0);        //
```































# WallPaper
> - wallpaper是一个service，被Launcher识别，加载到LivePicker列表中。
> - Launcher和动态壁纸的进程通过WallpaperManager进行进程间通信。

```
<service 
    android:label="@string/app_name"
      android:name=“.services.LiveWallpaper"
    android:icon=“@drawable/icon”
      android:permission=“android.permission.BIND_WALLPAPER"
    android:description="@string/wallpaper_description">
      <intent-filter>
        <action android:name="android.service.wallpaper.WallpaperService" />
      </intent-filter>
      <meta-data android:name="android.service.wallpaper" android:resource="@xml/livewallpaper" />
</service>
//res/xml/livewallpaper.xml
<wallpaper xmlns:android="http://schemas.android.com/apk/res/android"
    android:settingsActivity="com.beautyclocklivewallpaper.Settings"
    android:thumbnail="@drawable/icon"
/>


public class LiveWallpaper extends WallpaperService {
    @Override
    public Engine onCreateEngine() {
        return new BeautyClockEngine();
    }
}
class BeautyClockEngine extends Engine implements SharedPreferences.OnSharedPreferenceChangeListener {
    private Runnable drawRunnable = new Runnable() {
        public void run() {
            draw();
        }
    };
    private void draw() {
        SurfaceHolder holder = getSurfaceHolder();
        Canvas c = holder.lockCanvas();
    }
}


//andEngine
class LiveWallService extends org.andengine.extension.ui.livewallpaperBaseLiveWallpaperService
public EngineOptions onCreateEngineOptions() {}
public void onCreateResources(){}
public org.andengine.engine.Engine onCreateEngine(final EngineOptions pEngineOptions)
{
    return new org.andengine.engine.LimitedFPSEngine(pEngineOptions, MAX_FRAMES_PER_SECOND);        
}
```
















# WebView
> - 使用Html的Layout
> - 1.在src/main/asset/中添加html文件
> - 2.layout.xml添加webview

```
webView = (WebView)findViewById(R.id.webView);
webView.getSettings().setJavaScriptEnabled(true);
webView.getSettings().setSaveFormData(false);   //支持javascript
webView.getSettings().setSavePassword(false);   //支持表单
webView.getSettings().setSupportZoom(false);    //支持页面放大
webView.addjavascriptinterface(new MyJavaScript(), "itcast");
webView.loadUrl("file:///adroid_asset/index.html");


private final class MyJavaScript{
    public void call(final String phone){
        handler.post(new Runable(){
            @Overrid
            public void run(){
                Intent intent = new Intent(Intent.ACTION_CALL, Uri.parse("tel:"+phone));
                startActivity(intent);
            }
        });
    }
}

StaticLayout layout = new StaticLayout();
layout.draw(canvas);
```













# Drag&Drop

# Accessibility

# Style&Theme

> - Theme
> - res/values/style.xml

```
setTheme(R.style.Theme_Translucent2);

<style name="Theme.Translucent2">
    <item name="android:windowBackground">@drawable/pink</item>
    <item name="android:windowNoTitle">false</item>
    <item name="android:colorForeground">@drawable/darkgreen</item>
    <item name="android:colorBackground">@drawable/pink</item>
</style>
```
  

> - style
> - res/values/styles.xml

```
<style name="Theme.CustomDialog" parent="android:style/Theme.Dialog">
    <item name="andrid:windowBackground">@drawable/filled_box</item>
</style>
android:style/Theme.Dialog 对应于android.R.style.Theme_Dialog  //xml中用点.  , 代码中用_

<activity android:theme="@android:style/Theme.CustomDialog" />
或者    activity.setTheme(R.style.Theme_CustomeDialog);


///透明
<activity android:theme="@android:style/Theme.Translucent"

////桌面背景
<activity android:theme="@android:style/Theme.Wallpaper"
```







> - 扩展style,  自定义View
> - res/values/attrs.xml

```
<declare-styleable name="MyActionBar">
    <attr name="title" format="string" />
    <attr name="type">
        <enum name="normal" value="0" />
        <enum name="dashboard" value="1" />
        <enum name="empty" value="2" />
    </attr>
    <attr name="dividerDrawable" />
    <attr name="dividerWidth" />
    <attr name="homeDrawable" format="reference" />
    <attr name="maxItems" format="integer" />
</declare-styleable>





///values/gd_styles.xml
<style name="GreenDroid.Widget.MyActionBar">
    <item name="android:background">?attr/gdActionBarBackground</item>
    <item name="android:layout_height">@dimen/gd_action_bar_height</item>
    <item name="android:layout_width">fill_parent</item>
    <item name="dividerDrawable">?attr/gdActionBarDividerDrawable</item>
    <item name="dividerWidth">?attr/gdActionBarDividerWidth</item>
    <item name="homeDrawable">?attr/gdActionBarHomeDrawable</item>
    <item name="maxItems">?attr/gdActionBarMaxItems</item>
</style>
    



////layout
<greendroid.widget.MyActionBar
    style="@style/GreenDroid.Widget.MyActionBar"
    android:id="@id/gd_action_bar"
    android:layout_height="@dimen/gd_action_bar_height"
    android:layout_width="fill_parent"
    android:background="?attr/gdActionBarBackground" />




class MyActionBar extends LinearLayout{
    TypedArray a = context.obtainStyledAttributes(attrs, R.styleable.ActionBar, defStyle, 0);

    a.getString(R.styleable.ActionBar_title);
    a.getDrawable(R.styleable.ActionBar_dividerDrawable);
    a.getDimensionPixelSize(R.styleable.ActionBar_dividerWidth, -1);
    a.getDrawable(R.styleable.ActionBar_homeDrawable);
    a.getInt(R.styleable.ActionBar_maxItems, 3);
    a.recycle();
}
```




# Custom Component




