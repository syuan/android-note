
# Testing App Startup Performance

https://medium.com/androiddevelopers/testing-app-startup-performance-36169c27ee55

## ActivityTaskManager startup log

KitKat 부터는 logcat 를 통해서 Activity start time 을 확인할 수 있음.
start time 을 확인 할 수 있지만 logcat 을 읽어서 사용해야하기 때문에 자동화하기가 까다로움  
```
I/ActivityManager: Displayed com.coupang.mobile/.activity.SplashActivity: +3s157ms
```

## Shell Command for Testing Startup

adb shell 명령어 결과와 ActivityTaskManager logcat 결과는 동일  

```
$ adb shell am start-activity -W -n com.coupang.mobile/.domain.intro.SplashActivity

Starting: Intent { cmp=com.coupang.mobile/.domain.intro.SplashActivity }
Status: ok
Activity: com.coupang.mobile/.domain.intro.SplashActivity
ThisTime: 3157
TotalTime: 3157
WaitTime: 3185
Complete
```
> https://developer.android.com/studio/command-line/adb?hl=ko
> Activity Manager (am)
> -W : Wait for launch to complete.
> -n :  Specify the component name with package name prefix to create an explicit intent, such as "com.example.app/.ExampleActivity".

TotalTime 값만 가져오기 위해서 script 를 추가하면  
  
```
$ adb shell am start-activity -W -n com.coupang.mobile/.domain.intro.SplashActivity | grep "TotalTime" | cut -d ' ' -f 2

3157
```
  
cold start time 을 기준으로 측정하려면 앱을 완전히 종료 후에 다시 실행할 필요가 있음

```
$ adb shell am force-stop com.coupang.mobile
```

## Automating startup  


```
#!/bin/bash

for i in `seq 1 5`
do
  adb shell am force-stop com.coupang.mobile
  sleep 1
  adb shell am start-activity -W -n com.coupang.mobile/.domain.intro.SplashActivity | grep "TotalTime" | cut -d ' ' -f 2
done
```

파일로 출력 하려면
```
$ sh test.sh 2>&1 > test.log
$ cat test.log
2762
2795
2766
2739
2743
 ```

> $ ./gradlew lockClocks
> $ ./gradlew unlockClocks
  
  
## Test Results


|             | 6.4.0 |6.4.2 |
|-------------|-------|------|
|AVERAGE      | 301.87|202.47|
|PERCENTILE 50| 321   |171   |
|MIN          | 148   |143   |
|MAX          | 359   |171   |




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwOTI1MzkzMzIsMTA0MDk4ODg4MCwxMj
I3NDAxMDQwXX0=
-->