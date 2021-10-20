


## Send scheme with command line

> https://developer.android.com/studio/command-line/adb#IntentSpec


```bash
adb shell am start -a android.intent.action.VIEW -d market://details?id=krow.dev.scheme
```

#### Share text

android 에서 text 공유를 위해서 intent 를 만들면, 

```java
Intent intent = new Intent(Intent.ACTION_SEND);
intent.setType("text/html");
intent.putExtra(Intent.EXTRA_TEXT, "https://www.google.com");
```

Intent.EXTRA_TEXT 값은 
```java
public static final String EXTRA_TEXT = "android.intent.extra.TEXT";
```

이 동작을 adb 명령으로 바꾸면
```bash
adb shell am start -a android.intent.action.VIEW -t text/plain --es android.intent.extra.TEXT https://www.google.com
```


:frowning:  sms 로 전달해보면
```
adb shell am start -a android.intent.action.VIEW -t vnd.android-dir/mms-sms --es sms_body https://www.google.com
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMDk1NzI3MzksLTEzNjI4MzE0MTcsLT
IwNDM5ODczOTcsNDYyNjU0NjIxLC0xMzEyMDIzMjQ4LDE1NDE5
NjgzMl19
-->