

# Fatal Exception: kotlin.TypeCastException null cannot be cast to non-null type androidx.constraintlayout.widget.Guideline

```kotlin
Fatal Exception: kotlin.TypeCastException: null cannot be cast to non-null type androidx.constraintlayout.widget.Guideline
       at com.coupang.mobile.rds.units.snackbar.SnackBarContentView$text$1.run(SnackBarContentView.java:35)
       at android.os.Handler.handleCallback(Handler.java:938)
       at android.os.Handler.dispatchMessage(Handler.java:99)
       at android.os.Looper.loop(Looper.java:246)
       at android.app.ActivityThread.main(ActivityThread.java:8512)
       at java.lang.reflect.Method.invoke(Method.java)
       at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:602)
       at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1130)
```

kotlin synthetic 으로 선언된 변수가 null 을 반환해서 문제가 된 경우  
일반적인 경우는 synthetic 으로 사용되는 변수가 null 일 수 없음  

- 첫번째 의구심은 synthetic 으로 선언된 변수 중에서 하나는 null 이 아니였음
- 두번째 의구심은 synthetic 으로 선언된 변수가 null 이 될 수 있는가?

문제는 여러가지가 복합적인 문제

- view.post() 를 사용해서 동작을 lazy 하게 수행하는 코드에서 발생
- synthetic 을 사용해서 일바는 캐시에 저장된 변수를 사용
- Activity restore 과정에서 fragment 가 시스템에 의해서 되살아 났지만, fragment 를 새로 생성해서 replace
- onActivityCreated() 시점에 해당 코드 (스낵바를 보여주는) 를 수행


문제의 원인

- 문제는 Activity 가 restore 될때 발생
- Fragment 가 2번 생성되면서 onActivityCreated() 가 두번 불림
첫번째 Fragment 에 생성되어 스낵바를 생성하고 보여줄때, 일부 동작을 post() 로 수행
post 이전에는 뷰가 attach 되어 있어서 뷰들이 정상이고 사용한 일부 뷰는  synthetic 캐시에 저장됨
- 두번째 Fragment 로 replace 되면서 첫번재 Fragment 는 detach 되버림
- 첫번재 Fragment 가 detach 되었는데 첫번째 Fragment 의 post() 구분이 실행됨
- synthetic 에 캐시된 뷰는 null 이 아니지만 캐시가 안된 뷰는 null 이고 findViewById 로 찾으려 하지만 detach 되어서 뷰가 남아있지 않음, 그래서 null 이 반환됨

결론

- Frag
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY4OTUyOTI1Ml19
-->