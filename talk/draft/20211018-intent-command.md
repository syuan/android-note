


## Send scheme with command line

> https://developer.android.com/studio/command-line/adb#IntentSpec


```bash
adb shell am start -a android.intent.action.VIEW -d market://details?id=krow.dev.scheme
```

#### Share text

```java
Intent sharingIntent = new Intent(Intent.ACTION_SEND); sharingIntent.setType("text/html"); sharingIntent.putExtra(Intent.EXTRA_TEXT, "What you want to share");
```

```bash
adb shell am start -a android.intent.action.VIEW -t "text/plain" -d market://details?id=krow.dev.scheme
```


```
am start -a android.intent.action.VIEW -d com.glass.videoglass:// --ez startFromWS true
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzcwNDAzOTgzLC0xMzYyODMxNDE3LC0yMD
QzOTg3Mzk3LDQ2MjY1NDYyMSwtMTMxMjAyMzI0OCwxNTQxOTY4
MzJdfQ==
-->