


## Send scheme with command line

> https://developer.android.com/studio/command-line/adb#IntentSpec


```bash
adb shell am start -a android.intent.action.VIEW -d market://details?id=krow.dev.scheme
```

#### Share text

android intent 를 text share 
```java
Intent sharingIntent = new Intent(Intent.ACTION_SEND); sharingIntent.setType("text/html"); sharingIntent.putExtra(Intent.EXTRA_TEXT, "https://www.google.com");
```


```
public static final String EXTRA_TEXT = "android.intent.extra.TEXT";
```

```bash
adb shell am start -a android.intent.action.VIEW -t "text/plain" --es https%3A%2F%2Fwww.google.com
```

https://www.google.com
https%3A%2F%2Fwww.google.com

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NDE3MDc2MTYsLTEzNjI4MzE0MTcsLT
IwNDM5ODczOTcsNDYyNjU0NjIxLC0xMzEyMDIzMjQ4LDE1NDE5
NjgzMl19
-->