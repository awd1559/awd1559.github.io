---
layout:     post
title:      "volley"
subtitle:   " \"Android volley by google\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
---
><small>[volley](https://android.googlesource.com/platform/frameworks/volley)</small>
><small>目录:[gradle](/2014/06/09/gradle)</small>

# install
```
compile 'com.android.volley:volley:1.0.0'

# DEPRECATED
compile 'com.mcxiaoke.volley:library:1.0.19'


git clone https://android.googlesource.com/platform/frameworks/volley

<uses-permission android:name="android.permission.INTERNET"/>

```


# use java.net.HttpURLConnection

```
# android sdk use java.net.HttpURLConnection
HttpUrlConnection urlConnection = (HttpURLConnection) url.openConnection();
  try {
    urlConnection.setDoOutput(true);
    urlConnection.setChunkedStreamingMode(0);

    OutputStream out = new BufferedOutputStream(urlConnection.getOutputStream());
    writeStream(out);

    InputStream in = new BufferedInputStream(urlConnection.getInputStream());
    readStream(in);
  }finaly {
    urlConnection.disconnect();
}
```


# RequestQueue

```
RequestQueue mQueue = Volley.newRequestQueue(context);
```

# ImageLoader

```
LruBitmapCache  imageCache = new LruBitmapCache();
DiskBitmapCache imageCache = new DiskBitmapCache();

ImageLoader mImageLoader = new ImageLoader(mQueue, imageCache);

ImageLoader.ImageListener listener = ImageLoader.getImageListener(this.mImage, R.drawable.holder, R.drawable.error);
imageLoader.get(url, listener);
```

#### ImageListener

```
class FadeInImageListener implements ImageLoader.ImageListener {
	WeakReference<ImageView> mImageView;
	Context mContext;
	
	public FadeInImageListener(ImageView image,Context context) {
		mImageView = new WeakReference<ImageView>(image);
		mContext = context;
	}
	
	@Override
	public void onErrorResponse(VolleyError arg0) {
		if(mImageView.get() != null) {
			mImageView.get().setImageResource(R.drawable.ic_launcher);
		}
	}

	@Override
	public void onResponse(ImageContainer response, boolean arg1) {
		if(mImageView.get() != null) {
			ImageView image = mImageView.get();
			if(response.getBitmap() != null) {
                image.startAnimation(AnimationUtils.loadAnimation(mContext, R.anim.fade_in));
                image.setImageBitmap(response.getBitmap());
			} else {
				image.setImageResource(R.drawable.ic_launcher);
			}
		}
	}
}
```

#### StringRequest

```
String url = ”http://www.baidu.com”;
StringRequest stringRequest = new StringRequst(Request.Method.GET, url, 
  new Response.Listener<String>( {
    @Override
    public void onResponse(String reponse) {
    }
  }, 
  new Response.ErrorListener() {
    @Override
    public void onErrorResponse(VolleyError error) {}
  }));

mQueue.add(stringRequest);
```

#### JSONRequest

```

```

#### JsonArrayRequest

```
```

#### JsonObjectRequest

```
String url = "https://api.flickr.com/services/rest";
Uri.Builder builder = Uri.parse(url).buildUpon();
builder.appendQueryParameter("api_key", "5e045abd4baba4bbcd866e1864ca9d7b");
builder.appendQueryParameter("method", "flickr.interestingness.getList");
builder.appendQueryParameter("format", "json");
builder.appendQueryParameter("nojsoncallback", “1");

JsonObjectRequest jsonObjReq = new JsonObjectRequest(Method.GET, builder.toString(), null,
    new Response.Listener<JSONObject>() {
      @Override
      public void onResponse(JSONObject response) {
        Log.d(TAG, response.toString());
      }
    }, 
    new Response.ErrorListener() {
      @Override
      public void onErrorResponse(VolleyError error) {
        VolleyLog.d(TAG, "Error: " + error.getMessage());
      }
});

```

#### Request

```
public class GsonRequest<T> extends Request<T>{
  private final Gson gson;
  private final Response.Listener<T> listener;

  @Override
  protected void deliverResponse(T response) {
    listener.onResponse(response);
  }

  @Override
  protected Response<T> parseNetworkResponse(NetworkResponse response) {
    String json = new String(response.data, HttpHeaderParser.parseCharset(response.headers));

    return (Response<T>) Response.success(
                            gson.fromJson(json, type),
                            HttpHeaderParser.parseCacheHeaders(response));
  }
}



GsonRequest<Model> gsonObjRequest = new GsonRequest<Model>(Request.Method.GET, builder.toString(), 
  new Response.Listener<FlickrResponsePhotos>(){
    public void onResponse(Model response) {}
  }, 
  new Response.ErrorListener(){
    @Override
    public void onErrorResponse(VolleyError error) {
      if( error instanceof NetworkError) {} 
      else if( error instanceof ClientError) {} 
      else if( error instanceof ServerError) {} 
      else if( error instanceof AuthFailureError) {} 
      else if( error instanceof ParseError) {} 
      else if( error instanceof NoConnectionError) {} 
      else if( error instanceof TimeoutError) {}
    }
  });
```

#### cache

```
Cache cache = new DiskBasedCache(getCacheDir(), 1024 * 1024); 
Network network = new BasicNetwork(new HurlStack());
RequestQueue  mRequestQueue = new RequestQueue(cache, network);
mRequestQueue.start();
```


