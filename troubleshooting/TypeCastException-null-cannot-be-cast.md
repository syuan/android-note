

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

묹

<!--stackedit_data:
eyJoaXN0b3J5IjpbNzgzNjEyNDUxXX0=
-->