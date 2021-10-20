


## Send scheme with command line

> https://developer.android.com/studio/command-line/adb#IntentSpec



```
am start -a android.intent.action.VIEW -d com.glass.videoglass:// --ez startFromWS true
```

am start -a android.intent.action.MAIN -n com.example/com.example.MainActivity

서비스 실행
am startservice  -n [패키지명]/[패키지명 포함 서비스명]

브로드캐스트 보내기
am broadcast  -a [braodcast 명]
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDYyNjU0NjIxLC0xMzEyMDIzMjQ4LDE1ND
E5NjgzMl19
-->