


## Send scheme with command line

> https://developer.android.com/studio/command-line/adb#IntentSpec


```bash
adb shell am start -a android.intent.action.VIEW -d market://details?id=krow.dev.scheme
```

#### Share text

android 에서 text 공유를 위해서 intent 를 만들면, 
```java
Intent sharingIntent = new Intent(Intent.ACTION_SEND); sharingIntent.setType("text/html"); sharingIntent.putExtra(Intent.EXTRA_TEXT, "https://www.google.com");
```

Intent.EXTRA_TEXT 값은 
```
public static final String EXTRA_TEXT = "android.intent.extra.TEXT";
```

이 동작을 adb 명령으로 바꾸면
```bash
adb shell am start -a android.intent.action.VIEW -t text/plain --es android.intent.extra.TEXT https://www.google.com
```

adb shell am start -a android.intent.action.VIEW --es android.intent.extra.TEXT https://www.google.com


https://www.google.com
https%3A%2F%2Fwww.google.com

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA0NDc0NDk5MSwtMTM2MjgzMTQxNywtMj
A0Mzk4NzM5Nyw0NjI2NTQ2MjEsLTEzMTIwMjMyNDgsMTU0MTk2
ODMyXX0=
-->