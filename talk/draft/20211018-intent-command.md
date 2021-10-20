


## Send scheme with command line

> https://developer.android.com/studio/command-line/adb#IntentSpec


```bash
adb shell am start -a android.intent.action.VIEW -d market://details?id=krow.dev.scheme
```

#### Share text

```java
Intent sharingIntent = new Intent(Intent.ACTION_SEND); sharingIntent.setType("text/html"); sharingIntent.putExtra(Intent.EXTRA_TEXT, "https://www.google.com");
```

```bash
adb shell am start -a android.intent.action.VIEW -t "text/plain" --es https%3A%2F%2Fwww.google.com
```


```
am start -a android.intent.action.VIEW -d com.glass.videoglass:// --ez startFromWS true
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg3MDE5OTkzMCwtMTM2MjgzMTQxNywtMj
A0Mzk4NzM5Nyw0NjI2NTQ2MjEsLTEzMTIwMjMyNDgsMTU0MTk2
ODMyXX0=
-->