


## Send scheme with command line

> https://developer.android.com/studio/command-line/adb#IntentSpec


```
adb shell am start -a android.intent.action.VIEW -d market://details?id=krow.dev.scheme
```


```
am start -a android.intent.action.VIEW -d com.glass.videoglass:// --ez startFromWS true
```

am start -a android.intent.action.MAIN -n com.example/com.example.MainActivity

서비스 실행
am startservice  -n [패키지명]/[패키지명 포함 서비스명]

브로드캐스트 보내기
am broadcast  -a [braodcast 명]
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNjI4MzE0MTcsLTIwNDM5ODczOTcsND
YyNjU0NjIxLC0xMzEyMDIzMjQ4LDE1NDE5NjgzMl19
-->