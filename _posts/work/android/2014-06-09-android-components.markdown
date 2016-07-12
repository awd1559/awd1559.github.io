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

android.content.Context

| -------- | ------------ |
|Activity  |startActvity()|
|Service   |startService()<br>bindService()
|Broadcasts|sendBroadcasts()<br>sendOrderedBroadcasts()<br>sendStickyBroadcasts()

- 显式Intent

```
Intent downloadIntent = new Intent(this, DownloadService.class);
startService(downloadIntent);
```

- 隐式Intent

```
Intent sendIntent = new Intent();
sendIntent.setAction(Intent.ACTION_SEND);
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
sendIntent.setType("text/plain");

// Verify that the intent will resolve to an activity
if (sendIntent.resolveActivity(getPackageManager()) != null) {
    startActivity(sendIntent);
}


//force to use application chooser
Intent intent = new Intent(Intent.ACTION_SEND);
....
Intent chooser = Intent.createChooser(intent, title);
if (sendIntent.resolveActivity(getPackageManager()) != null) {
    startActivity(sendIntent);
}
```



#### action

- standard activity actions<br>
for ACTION_*: android.intent.action.*
example: ACTION_MAIN, android.intent.action.MAIN

| ------------------ | -------|
|ACTION_MAIN         ||
|ACTION_VIEW         ||
|ACTION_ATTACH_DATA  ||
|ACTION_EDIT         ||
|ACTION_PICK         ||
|ACTION_CHOOSER      ||
|ACTION_GET_CONTENT  ||
|ACTION_DIAL         ||
|ACTION_CALL         ||
|ACTION_SEND         ||
|ACTION_SENDTO       ||
|ACTION_ANSWER       ||
|ACTION_INSERT       ||
|ACTION_DELETE       ||
|ACTION_RUN          ||
|ACTION_SYNC         ||
|ACTION_PICK_ACTIVITY||
|ACTION_SEARCH       ||
|ACTION_WEB_SEARCH   ||
|ACTION_FACTORY_TEST ||

- standard broadcast cation

| ------------------------- | --------- |
|ACTION_TIME_TICK           |
|ACTION_TIME_CHANGED        |
|ACTION_TIMEZONE_CHANGED    |
|ACTION_BOOT_COMPLETED      |
|ACTION_PACKAGE_ADDED       |
|ACTION_PACKAGE_CHANGED     |
|ACTION_PACKAGE_REMOVED     |
|ACTION_PACKAGE_RESTARTED   |
|ACTION_PACKAGE_DATA_CLEARED|
|ACTION_UID_REMOVED         |
|ACTION_BATTERY_CHANGED     |
|ACTION_POWER_CONNECTED     |
|ACTION_POWER_DISCONNECTED  |
|ACTION_SHUTDOWN            |

```
intent.setAction(String action)
```
  custom action


#### category

- standard categories
for CATEGORY_*: android.intent.category.*
example: CATEGORY_DEFAULT, android.intent.category.DEFAULT

| --------------------------- | --------------- |
|CATEGORY_DEFAULT             |
|CATEGORY_BROWSABLE           |
|CATEGORY_TAB                 |
|CATEGORY_ALTERNATIVE         |
|CATEGORY_SELECTED_ALTERNATIVE|
|CATEGORY_LAUNCHER            |
|CATEGORY_INFO                |
|CATEGORY_HOME                |
|CATEGORY_PREFERENCE          |
|CATEGORY_TEST                |
|CATEGORY_CAR_DOCK            |
|CATEGORY_DESK_DOCK           |
|CATEGORY_LE_DESK_DOCK        |
|CATEGORY_HE_DESK_DOCK        |
|CATEGORY_CAR_MODE            |
|CATEGORY_APP_MARKET          |

```
intent.addCategory()
intent.removeCategory()
```

#### extras

standard extra data
| -------------------------- | -----------|
|EXTRA_ALARM_COUNT           |
|EXTRA_BCC                   |
|EXTRA_CC                    |
|EXTRA_CHANGED_COMPONENT_NAME|
|EXTRA_DATA_REMOVED          |
|EXTRA_DOCK_STATE            |
|EXTRA_DOCK_STATE_HE_DESK    |
|EXTRA_DOCK_STATE_LE_DESK    |
|EXTRA_DOCK_STATE_CAR        |
|EXTRA_DOCK_STATE_DESK       |
|EXTRA_DOCK_STATE_UNDOCKED   |
|EXTRA_DONT_KILL_APP         |
|EXTRA_EMAIL                 |
|EXTRA_INITIAL_INTENTS       |
|EXTRA_INTENT                |
|EXTRA_KEY_EVENT             |
|EXTRA_ORIGINATING_URI       |
|EXTRA_PHONE_NUMBER          |
|EXTRA_REFERRER              |
|EXTRA_REMOTE_INTENT_TOKEN   |
|EXTRA_REPLACING             |
|EXTRA_SHORTCUT_ICON         |
|EXTRA_SHORTCUT_ICON_RESOURCE|
|EXTRA_SHORTCUT_INTENT       |
|EXTRA_STREAM                |
|EXTRA_SHORTCUT_NAME         |
|EXTRA_SUBJECT               |
|EXTRA_TEMPLATE              |
|EXTRA_TEXT                  |
|EXTRA_TITLE                 |
|EXTRA_UID                   |

```
putExtra(String name, bool value)
putExtra(String name, int[] value)
.....

putExtra(String name, Bundle value)


Bundle getExtras()
  //getExtras().getLong(String key)
  //getExtras().getDouble(String key)
getFloatArrayExtra(String name)
getFloatExtra(String name, float defaultValue)
getIntExtra(String name, int defaultValue)
```

#### data


```
Uri uri =  Uri.parse("file://com.android.test:520/mnt/sdcard");
intent.setData(uri)
intent.setType(String ); //Set an explicit MIME data typ

```

  


#### intent filter

- action 测试
- category 测试
- data 测试

<intent-filter>
  <action android:name="android.intent.action.SEND"/>
  <action android:name="android.intent.action.SEND_MULTIPLE"/>
  <category android:name="android.intent.category.DEFAULT"/>
  <data android:scheme="file"/>
  <data android:host="" android:port/>
  <data android:path=""/>
  <data android:mimeType="image/*"/>
</intent-filter>
scheme://host:port/path


#### Pending Intent


# Comment Intent

#### Alarm Clock

```
//create an alarm
new Intent(AlarmClock.ACTION_SET_ALARM)
            .putExtra(AlarmClock.EXTRA_MESSAGE, message)
            .putExtra(AlarmClock.EXTRA_HOUR, hour)
            .putExtra(AlarmClock.EXTRA_MINUTES, minutes);
<uses-permission android:name="com.android.alarm.permission.SET_ALARM" />
<action android:name="android.intent.action.SET_ALARM" />
```

- Extras

- EXTRA_HOUR<br>
  The hour for the alarm.

- EXTRA_MINUTES<br>
  The minutes for the alarm.

- EXTRA_MESSAGE<br>
  A custom message to identify the alarm.

- EXTRA_DAYS<br>
  An ArrayList including each week day on which this alarm should be repeated. <br>
  Each day must be declared with an integer from the Calendar class such as MONDAY.<br>
  For a one-time alarm, do not specify this extra.

- EXTRA_RINGTONE<br>
  A content: URI specifying a ringtone to use with the alarm, or VALUE_RINGTONE_SILENT for no ringtone.
  To use the default ringtone, do not specify this extra.

- EXTRA_VIBRATE<br>
A boolean specifying whether to vibrate for this alarm.

- EXTRA_SKIP_UI<br>
A boolean specifying whether the responding app should skip its UI when setting the alarm. If true, the app should bypass any confirmation UI and simply set the specified alarm.

```
//create a timer
intent = new Intent(AlarmClock.ACTION_SET_TIMER)
       .putExtra(AlarmClock.EXTRA_MESSAGE, message)
            .putExtra(AlarmClock.EXTRA_LENGTH, seconds)
            .putExtra(AlarmClock.EXTRA_SKIP_UI, true);
<uses-permission android:name="com.android.alarm.permission.SET_ALARM" />
<action android:name="android.intent.action.SET_TIMER" />
```
- Extras
- EXTRA_LENGTH<br>
  The length of the timer in seconds.
- EXTRA_MESSAGE<br>
  A custom message to identify the timer.
- EXTRA_SKIP_UI<br>
  A boolean specifying whether the responding app should skip its UI when setting the timer. If true, the app should bypass any confirmation UI and simply start the specified timer.

```
//show all alarms
<action android:name="android.intent.action.SHOW_ALARMS" />
```



#### Calendar

```
//add a calendar event
new Intent(Intent.ACTION_INSERT)
            .setData(Events.CONTENT_URI)
            .putExtra(Events.TITLE, title)
            .putExtra(Events.EVENT_LOCATION, location)
            .putExtra(CalendarContract.EXTRA_EVENT_BEGIN_TIME, begin)
            .putExtra(CalendarContract.EXTRA_EVENT_END_TIME, end);
<action android:name="android.intent.action.INSERT" />
<data android:mimeType="vnd.android.cursor.dir/event" />
```

- Action<br>
  ACTION_INSERT
- Data URI<br>
  Events.CONTENT_URI
- MIME Type<br>
  "vnd.android.cursor.dir/event"
- Extras<br>
- EXTRA_EVENT_ALL_DAY<br>
  A boolean specifying whether this is an all-day event.
- EXTRA_EVENT_BEGIN_TIME<br>
  The start time of the event (milliseconds since epoch).
- EXTRA_EVENT_END_TIME<br>
  The end time of the event (milliseconds since epoch).
- TITLE<br>
  The event title.
- DESCRIPTION<br>
  The event description.
- EVENT_LOCATION<br>
  The event location.
- EXTRA_EMAIL<br>
  A comma-separated list of email addresses that specify the invitees.
  Many more event details can be specified using the constants defined in the CalendarContract.EventsColumns class.


#### Camera

```
//capture a picture or video and return it
new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
intent.putExtra(MediaStore.EXTRA_OUTPUT, Uri.withAppendedPath(mLocationForPhotos, targetFilename);
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == REQUEST_IMAGE_CAPTURE && resultCode == RESULT_OK) {
  Bitmap thumbnail = data.getParcelable("data");
  // Do other work with full size photo saved in mLocationForPhotos
        ...
  }
}

<action android:name="android.media.action.IMAGE_CAPTURE" />
```

- Action<br>
  ACTION_IMAGE_CAPTURE<br>
  ACTION_VIDEO_CAPTURE
- Extras<br>
- EXTRA_OUTPUT<br>
  The URI location where the camera app should save the photo or video file (as a Uri object).


```
//start a camera app in still image mode
new Intent(MediaStore.INTENT_ACTION_STILL_IMAGE_CAMERA);
<action android:name="android.media.action.STILL_IMAGE_CAMERA" />

//start a camera app in video mode
new Intent(MediaStore.INTENT_ACTION_VIDEO_CAMERA);
<action android:name="android.media.action.VIDEO_CAMERA" />
```


#### Contacts

```
//select a contact
new Intent(Intent.ACTION_PICK);
intent.setType(ContactsContract.Contacts.CONTENT_TYPE);
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
  if (requestCode == REQUEST_SELECT_CONTACT && resultCode == RESULT_OK) {
    Uri contactUri = data.getData();
    // Do something with the selected contact at contactUri
    ...
  }
}
```

- MIME Type<br>
  Contacts.CONTENT_TYPE


```
//select specific contact data
new Intent(Intent.ACTION_PICK);
intent.setType(CommonDataKinds.Phone.CONTENT_TYPE);
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
  if (requestCode == REQUEST_SELECT_PHONE_NUMBER && resultCode == RESULT_OK) {
    // Get the URI and query the content provider for the phone number
    Uri contactUri = data.getData();
    String[] projection = new String[]{CommonDataKinds.Phone.NUMBER};
    Cursor cursor = getContentResolver().query(contactUri, projection,null, null, null);
    // If the cursor returned is valid, get the phone number
    if (cursor != null && cursor.moveToFirst()) {
      int numberIndex = cursor.getColumnIndex(CommonDataKinds.Phone.NUMBER);
      String number = cursor.getString(numberIndex);
      // Do something with the phone number
      ...
    }
  }
}
```

- MIME Type<br>
- CommonDataKinds.Phone.CONTENT_TYPE<br>
  Pick from contacts with a phone number.
- CommonDataKinds.Email.CONTENT_TYPE<br>
  Pick from contacts with an email address.
- CommonDataKinds.StructuredPostal.CONTENT_TYPE<br>
  Pick from contacts with a postal address.<br>
  Or one of many other CONTENT_TYPE values under ContactsContract.

```
//view a contact
new Intent(Intent.ACTION_VIEW, contactUri);
```

- Data URI Scheme<br>
  content:<URI>

```
//edit an existing contact
new Intent(Intent.ACTION_EDIT);
intent.setData(contactUri);
intent.putExtra(Intents.Insert.EMAIL, email);
```

- Data URI Scheme<br>
  content:<URI>
- MIME Type<br>
  The type is inferred from contact URI.
- Extras<br>
  One or more of the extras defined in ContactsContract.Intents.Insert so you can populate fields of the contact details.


```
//insert a contact
new Intent(Intent.ACTION_INSERT);
intent.setType(Contacts.CONTENT_TYPE);
intent.putExtra(Intents.Insert.NAME, name);
intent.putExtra(Intents.Insert.EMAIL, email);
```

- MIME Type<br>
  Contacts.CONTENT_TYPE
- Extras<br>
  One or more of the extras defined in ContactsContract.Intents.Insert.


#### Email

```
//compose an email with optional attachments
new Intent(Intent.ACTION_SEND);
intent.setType("*/*");
intent.putExtra(Intent.EXTRA_EMAIL, addresses);
intent.putExtra(Intent.EXTRA_SUBJECT, subject);
intent.putExtra(Intent.EXTRA_STREAM, attachment);
<intent-filter>
  <action android:name="android.intent.action.SEND" />
  <data android:type="*/*" />
  <category android:name="android.intent.category.DEFAULT" />
</intent-filter>
<intent-filter>
  <action android:name="android.intent.action.SENDTO" />
  <data android:scheme="mailto" />
  <category android:name="android.intent.category.DEFAULT" />
</intent-filter>
```

- Action<br>
  ACTION_SENDTO (for no attachment) or<br>
  ACTION_SEND (for one attachment) or<br>
  ACTION_SEND_MULTIPLE (for multiple attachments)
- Data URI Scheme<br>
  None
- MIME Type<br>
  PLAIN_TEXT_TYPE ("text/plain")<br>
  "*/*"
- Extras<br>
- Intent.EXTRA_EMAIL<br>
  A string array of all "To" recipient email addresses.
- Intent.EXTRA_CC<br>
  A string array of all "CC" recipient email addresses.
- Intent.EXTRA_BCC<br>
  A string array of all "BCC" recipient email addresses.
- Intent.EXTRA_SUBJECT<br>
  A string with the email subject.
- Intent.EXTRA_TEXT<br>
  A string with the body of the email.
- Intent.EXTRA_STREAM<br>
  A Uri pointing to the attachment. If using the ACTION_SEND_MULTIPLE action, this should instead be an ArrayList containing multiple Uri objects.





#### File Storage

```
//retrieve a specific type of file
new Intent(Intent.ACTION_GET_CONTENT);
intent.setType(“image/*");
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == REQUEST_IMAGE_GET && resultCode == RESULT_OK) {
        Bitmap thumbnail = data.getParcelable("data");
        Uri fullPhotoUri = data.getData();
        // Do work with photo saved at fullPhotoUri
        ...
    }
}
    <intent-filter>
        <action android:name="android.intent.action.GET_CONTENT" />
        <data android:type="image/*" />
        <category android:name="android.intent.category.DEFAULT" />
        <!-- The OPENABLE category declares that the returned file is accessible
             from a content provider that supports OpenableColumns
             and ContentResolver.openFileDescriptor() -->
        <category android:name="android.intent.category.OPENABLE" />
    </intent-filter>
```

- Extras<br>
- EXTRA_ALLOW_MULTIPLE<br>
  A boolean declaring whether the user can select more than one file at a time.
- EXTRA_LOCAL_ONLY<br>
  A boolean that declares whether the returned file must be available directly from the device, rather than requiring a download from a remote service.
- Category (optional)<br>
- CATEGORY_OPENABLE<br>
  To return only "openable" files that can be represented as a file stream with openFileDescriptor().

```
//open a specific type of file
Intent intent = new Intent(Intent.ACTION_OPEN_DOCUMENT);
intent.setType("image/*");
intent.addCategory(Intent.CATEGORY_OPENABLE);
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == REQUEST_IMAGE_OPEN && resultCode == RESULT_OK) {
        Uri fullPhotoUri = data.getData();
        // Do work with full size photo saved at fullPhotoUri
        ...
    }
}
<provider ...
    android:grantUriPermissions="true"
    android:exported="true"
    android:permission="android.permission.MANAGE_DOCUMENTS">
    <intent-filter>
        <action android:name="android.content.action.DOCUMENTS_PROVIDER" />
    </intent-filter>
</provider>
```

- Action<br>
  ACTION_OPEN_DOCUMENT or<br>
  ACTION_CREATE_DOCUMENT
- MIME Type<br>
  The MIME type corresponding to the file type the user should select.
- Extras<br>
- EXTRA_MIME_TYPES<br>
  An array of MIME types corresponding to the types of files your app is requesting. When you use this extra, you must set the primary MIME type in setType() to "*/*".
- EXTRA_ALLOW_MULTIPLE<br>
  A boolean that declares whether the user can select more than one file at a time.
- EXTRA_TITLE<br>
  For use with ACTION_CREATE_DOCUMENT to specify an initial file name.
- EXTRA_LOCAL_ONLY<br>
  A boolean that declares whether the returned file must be available directly from the device, rather than requiring a download from a remote service.
- Category<br>
- CATEGORY_OPENABLE<br>
  To return only "openable" files that can be represented as a file stream with openFileDescriptor().


#### Maps

```
//show a location on a map
new Intent(Intent.ACTION_VIEW);
intent.setData(geoLocation);
<intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <data android:scheme="geo" />
        <category android:name="android.intent.category.DEFAULT" />
</intent-filter>
```

- Action<br>
- ACTION_VIEW<br>
- Data URI Scheme<br>
  geo:latitude,longitude<br>
  Show the map at the given longitude and latitude.<br>
  Example: "geo:47.6,-122.3"<br>
  geo:latitude,longitude?z=zoom<br>
  Show the map at the given longitude and latitude at a certain zoom level. A zoom level of 1 shows the whole Earth, centered at the given lat,lng. The highest (closest) zoom level is 23.<br>
  Example: "geo:47.6,-122.3?z=11"<br>
  geo:0,0?q=lat,lng(label)<br>
  Show the map at the given longitude and latitude with a string label.<br>
  Example: "geo:0,0?q=34.99,-106.61(Treasure)"<br>
  geo:0,0?q=my+street+address<br>
  Show the location for "my street address" (may be a specific address or location query).<br>
  Example: "geo:0,0?q=1600+Amphitheatre+Parkway%2C+CA"<br>
  Note: All strings passed in the geo URI must be encoded. For example, the string 1st & Pike, Seattle should become 1st%20%26%20Pike%2C%20Seattle. Spaces in the string can be encoded with %20 or replaced with the plus sign (+).


#### Music or Video

```
//paly a media file
new Intent(Intent.ACTION_VIEW);
intent.setData(file);
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <data android:type="audio/*" />
        <data android:type="application/ogg" />
        <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
```

- Action<br>
- ACTION_VIEW<br>
- Data URI Scheme<br>
  file:<URI><br>
  content:<URI><br>
  http:<URL><br>
- MIME Type<br>
  "audio/*"<br>
  "application/ogg"<br>
  "application/x-ogg"<br>
  "application/itunes"<br>
  Or any other that your app may require.

```
//play music based on search query
new Intent(MediaStore.INTENT_ACTION_MEDIA_PLAY_FROM_SEARCH);
intent.putExtra(MediaStore.EXTRA_MEDIA_FOCUS,MediaStore.Audio.Artists.ENTRY_CONTENT_TYPE);
intent.putExtra(MediaStore.EXTRA_MEDIA_ARTIST, artist);
intent.putExtra(SearchManager.QUERY, artist);
<action android:name="android.media.action.MEDIA_PLAY_FROM_SEARCH" />
```

When handling this intent, your activity should check the value of the EXTRA_MEDIA_FOCUS extra in the incoming Intent to determine the search mode. Once your activity has identified the search mode, it should read the values of the additional extras for that particular search mode. With this information your app can then perform the search within its inventory to play the content that matches the search query. For example:

```
protected void onCreate(Bundle savedInstanceState) {
    ...
    Intent intent = this.getIntent();
    if (intent.getAction().compareTo(MediaStore.INTENT_ACTION_MEDIA_PLAY_FROM_SEARCH) == 0) {

        String mediaFocus = intent.getStringExtra(MediaStore.EXTRA_MEDIA_FOCUS);
        String query = intent.getStringExtra(SearchManager.QUERY);

        // Some of these extras may not be available depending on the search mode
        String album = intent.getStringExtra(MediaStore.EXTRA_MEDIA_ALBUM);
        String artist = intent.getStringExtra(MediaStore.EXTRA_MEDIA_ARTIST);
        String genre = intent.getStringExtra("android.intent.extra.genre");
        String playlist = intent.getStringExtra("android.intent.extra.playlist");
        String title = intent.getStringExtra(MediaStore.EXTRA_MEDIA_TITLE);

        // Determine the search mode and use the corresponding extras
        if (mediaFocus == null) {
            // 'Unstructured' search mode (backward compatible)
            playUnstructuredSearch(query);

        } else if (mediaFocus.compareTo("vnd.android.cursor.item/*") == 0) {
            if (query.isEmpty()) {
                // 'Any' search mode
                playResumeLastPlaylist();
            } else {
                // 'Unstructured' search mode
                playUnstructuredSearch(query);
            }

        } else if (mediaFocus.compareTo(MediaStore.Audio.Genres.ENTRY_CONTENT_TYPE) == 0) {
            // 'Genre' search mode
            playGenre(genre);

        } else if (mediaFocus.compareTo(MediaStore.Audio.Artists.ENTRY_CONTENT_TYPE) == 0) {
            // 'Artist' search mode
            playArtist(artist, genre);

        } else if (mediaFocus.compareTo(MediaStore.Audio.Albums.ENTRY_CONTENT_TYPE) == 0) {
            // 'Album' search mode
            playAlbum(album, artist);

        } else if (mediaFocus.compareTo("vnd.android.cursor.item/audio") == 0) {
            // 'Song' search mode
            playSong(album, artist, genre, title);

        } else if (mediaFocus.compareTo(MediaStore.Audio.Playlists.ENTRY_CONTENT_TYPE) == 0) {
            // 'Playlist' search mode
            playPlaylist(album, artist, genre, playlist, title);
        }
    }
}
```


- Action<br>
- INTENT_ACTION_MEDIA_PLAY_FROM_SEARCH<br>
- Extras<br>
  MediaStore.EXTRA_MEDIA_FOCUS (required)<br>
  Indicates the search mode (whether the user is looking for a particular artist, album, song, or playlist). Most search modes take additional extras. For example, if the user is interested in listening to a particular song, the intent might have three additional extras: the song title, the artist, and the album. This intent supports the following search modes for each value of EXTRA_MEDIA_FOCUS:<br>
  Any - "vnd.android.cursor.item/*"<br>
  Play any music. The receiving app should play some music based on a smart choice, such as the last playlist the user listened to.<br>
  Additional extras:<br>
  • QUERY (required) - An empty string. This extra is always provided for backward compatibility: existing apps that do not know about search modes can process this intent as an unstructured search.<br>
  Unstructured - "vnd.android.cursor.item/*"<br>
  Play a particular song, album or genre from an unstructured search query. Apps may generate an intent with this search mode when they can't identify the type of content the user wants to listen to. Apps should use more specific search modes when possible.
Additional extras:
  • QUERY (required) - A string that contains any combination of: the artist, the album, the song name, or the genre.
Genre - Audio.Genres.ENTRY_CONTENT_TYPE
Play music of a particular genre.
Additional extras:
  • "android.intent.extra.genre" (required) - The genre.
  • QUERY (required) - The genre. This extra is always provided for backward compatibility: existing apps that do not know about search modes can process this intent as an unstructured search.
Artist - Audio.Artists.ENTRY_CONTENT_TYPE
Play music from a particular artist.
Additional extras:
  • EXTRA_MEDIA_ARTIST (required) - The artist.
  • "android.intent.extra.genre" - The genre.
  • QUERY (required) - A string that contains any combination of the artist or the genre. This extra is always provided for backward compatibility: existing apps that do not know about search modes can process this intent as an unstructured search.
Album - Audio.Albums.ENTRY_CONTENT_TYPE
Play music from a particular album.
Additional extras:
  • EXTRA_MEDIA_ALBUM (required) - The album.
  • EXTRA_MEDIA_ARTIST - The artist.
  • "android.intent.extra.genre" - The genre.
  • QUERY (required) - A string that contains any combination of the album or the artist. This extra is always provided for backward compatibility: existing apps that do not know about search modes can process this intent as an unstructured search.
Song - "vnd.android.cursor.item/audio"
Play a particular song.
Additional extras:
  • EXTRA_MEDIA_ALBUM - The album.
  • EXTRA_MEDIA_ARTIST - The artist.
  • "android.intent.extra.genre" - The genre.
  • EXTRA_MEDIA_TITLE (required) - The song name.
  • QUERY (required) - A string that contains any combination of: the album, the artist, the genre, or the title. This extra is always provided for backward compatibility: existing apps that do not know about search modes can process this intent as an unstructured search.
Playlist - Audio.Playlists.ENTRY_CONTENT_TYPE
Play a particular playlist or a playlist that matches some criteria specified by additional extras.
Additional extras:
  • EXTRA_MEDIA_ALBUM - The album.
  • EXTRA_MEDIA_ARTIST - The artist.
  • "android.intent.extra.genre" - The genre.
  • "android.intent.extra.playlist" - The playlist.
  • EXTRA_MEDIA_TITLE - The song name that the playlist is based on.
  • QUERY (required) - A string that contains any combination of: the album, the artist, the genre, the playlist, or the title. This extra is always provided for backward compatibility: existing apps that do not know about search modes can process this intent as an unstructured search.





#### Phone

```
//Initiate a phone call
new Intent(Intent.ACTION_DIAL);
intent.setData(Uri.parse("tel:" + phoneNumber));
<uses-permission android:name="android.permission.CALL_PHONE" />
```

- Action<br>
- ACTION_DIAL<br>
  Opens the dialer or phone app.
- ACTION_CALL<br>
  Places a phone call (requires the CALL_PHONE permission)
- Data URI Scheme<br>
  tel:<phone-number><br>
  voicemail:<phone-number>



#### Settings

```
//Open a specific section of settings
new Intent(Intent.ACTION_WIFI_SETTINGS);
```

- Action
- ACTION_SETTINGS
- ACTION_WIRELESS_SETTINGS
- ACTION_AIRPLANE_MODE_SETTINGS
- ACTION_WIFI_SETTINGS
- ACTION_APN_SETTINGS
- ACTION_BLUETOOTH_SETTINGS
- ACTION_DATE_SETTINGS
- ACTION_LOCALE_SETTINGS
- ACTION_INPUT_METHOD_SETTINGS
- ACTION_DISPLAY_SETTINGS
- ACTION_SECURITY_SETTINGS
- ACTION_LOCATION_SOURCE_SETTINGS
- ACTION_INTERNAL_STORAGE_SETTINGS
- ACTION_MEMORY_CARD_SETTINGS
See the Settings documentation for additional settings screens that are available.




#### Text Messageing

```
//compose an SMS/MMS message with attachment
new Intent(Intent.ACTION_SEND);
intent.setData(Uri.parse("smsto:"));  // This ensures only SMS apps respond
intent.putExtra("sms_body", message);
intent.putExtra(Intent.EXTRA_STREAM, attachment);
    <intent-filter>
        <action android:name="android.intent.action.SEND" />
        <data android:type="text/plain" />
        <data android:type="image/*" />
        <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
```

- Action
  ACTION_SENDTO or<br>
  ACTION_SEND or<br>
  ACTION_SEND_MULTIPLE
- Data URI Scheme
  sms:<phone_number><br>
  smsto:<phone_number><br>
  mms:<phone_number><br>
  mmsto:<phone_number><br>
  Each of these schemes are handled the same.
- MIME Type
  PLAIN_TEXT_TYPE ("text/plain")<br>
  "image/*"<br>
  "video/*"
- Extras
  "subject"<br>
  A string for the message subject (usually for MMS only).<br>
  "sms_body"<br>
  A string for the text message.
- EXTRA_STREAM
  A Uri pointing to the image or video to attach. If using the ACTION_SEND_MULTIPLE action, this extra should be an ArrayList of Uris pointing to the images/videos to attach.


#### Web Browser

```
//load a web URL
 Uri webpage = Uri.parse(url);
 Intent intent = new Intent(Intent.ACTION_VIEW, webpage);
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <!-- Include the host attribute if you want your app to respond
             only to URLs with your app's domain. -->
        <data android:scheme="http" android:host="www.example.com" />
        <category android:name="android.intent.category.DEFAULT" />
        <!-- The BROWSABLE category is required to get links from web pages. -->
        <category android:name="android.intent.category.BROWSABLE" />
    </intent-filter>
```

- Action
- ACTION_VIEW
- Data URI Scheme
  http:<URL><br>
  https:<URL>
- MIME Type
  PLAIN_TEXT_TYPE ("text/plain")<br>
  "text/html"<br>
  "application/xhtml+xml"<br>
  "application/vnd.wap.xhtml+xml"


```
//Perform a web search
new Intent(Intent.ACTION_SEARCH);
intent.putExtra(SearchManager.QUERY, query);
```

- Extras
  SearchManager.QUERY<br>
  The search string.<br>


# Activity

#### life cycle

| -------------------- | ----------------------------- |
|onCreate              |activity first launched,
|onRestart             |stopped activity become front
|onStart               |ui loaded,visiable
|onResume              |interact
|onPause               |out of focus, visiable, save instance state here, for example: unsaved db record 
|onStop                |unvisiable,do not run if no memory
|onDestroy             |destroy, do not run if no memory
|||
|onSaveInstanceState   |activity被杀死前，在onPause调用前调用，保存临时状态
|onRestoreInstanceState|保存一些在对ondestroy和oncreate方法的多次调用中需要保持的数据
|onNewIntent           |


#### background translucent

'''
#styles.xml
<style name="AppTheme.translucent" parent="AppTheme">
        <item name="android:windowBackground">@color/translucent_background</item>
    <item name="android:windowIsTranslucent">true</item>
</style>
#colors.xml
<color name="translucent_background">#60000000</color>
'''

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

#### parameter

```
Intent intent = new Intent(ReceiveResult.this, SendResult.class);
startActivityForResult(intent, int GET_CODE);

void onActivityResult(int requestCode, int resultCode, Intent data) {
  //是从SendResult返回的
  if (requestCode == GET_CODE) 
  //返回的结果代码
  if (resultCode == RESULT_OK)
  //返回的Intent
  data.getAction();
}


//SendResult.java
setResult(RESULT_OK, (new Intent()).setAction("Corky!"));
finish();
```


#### configuration changes

```
//restore the activity state
onSaveInstanceState(Bundle outState, PersistableBundle out);
onRestoreInstanceState(Bundle savedInstanceState);
```

# Framgment

#### Life Cycle

#### Type
- DialogFragment
- ListFragment
- PreferenceFragment

#### Create

```

MyDialogFragment extends DialogFragment{
  @Override
  public Dialog onCreate(Bundle savedInstanceState) ｛
    int title = getArguments().getInt("title");
  }

  @Override
  public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    return inflater.inflate(R.layout.frag_mydialog, container);
  }
}

MyDialogFragment mydialog = new MyDialogFragment();
Bundle args = new Bundle();
args.putInt("title", title);
mydialog.setArguments(args);
mydialog.show(getSupportFragmentManager(), "mydialog");


FragmentTransaction ft = getSupportFragmentManager().beginTransaction();

MyFragment f = Fragment.instantiate(context,  MyFragment.getName(),  args);
MyFragment f = new MyFragment();

ft.add(containerID, f);

```


#### add to activity

```
FragmentTransaction ft = getSupportFragmentManager().beginTransaction();
ft.add(containerID, fragment)
ft.replace(id, fragment)
//add fragment without ui, use tag
add(fragment, tag);

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
ft.add(containerID, fragment);
ft.addToBackStack(null);
ft.attach(fragment);
ft.detach(fragment);
ft.show(fragment);
ft.hide(fragment);
ft.remove(fragment);
ft.replace(containerID, fragment);
ft.setCustomeAnimations(enter, exit);
ft.Transition(transit);
ft.setTransitionStyle(styleID);
ft.commit();
```


# Loader

# Service

service do not start a thread, can assigned to run a specific thread

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


