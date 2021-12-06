
# NullPointerException: Attempt to invoke virtual method 'void com.android.server.wm.ActivityRecord.addTargetSplitActivities

```java
Caused by java.lang.NullPointerException: Attempt to invoke virtual method 'void com.android.server.wm.ActivityRecord.addTargetSplitActivities(com.android.server.wm.ActivityRecord)' on a null object reference
       at android.os.Parcel.createExceptionOrNull(Parcel.java:2391)
       at android.os.Parcel.createException(Parcel.java:2369)
       at android.os.Parcel.readException(Parcel.java:2352)
       at android.os.Parcel.readException(Parcel.java:2294)
       at android.app.IActivityTaskManager$Stub$Proxy.finishActivity(IActivityTaskManager.java:5047)
       at android.app.Activity.finish(Activity.java:6457)
       at android.app.Activity.finish(Activity.java:6493)
       ...
```


https://stackoverflow.com/questions/18858320/nullpointerexception-etc-from-parcel-readexception

try-catch 걸어야하나?



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMzNzcxMTA2M119
-->