
# Activity.isFinishing


> android.view.WindowManager$**BadTokenException**: Unable to add window – token android.os.BinderProxy@40b47bd8 is not valid; is your activity running?

> java.lang.RuntimeException: java.lang.IllegalArgumentException: You cannot start a load for a destroyed activity  
>  https://github.com/bumptech/glide/issues/1126  


### isFinishing()

  
#### 
```java
public boolean isFinishing() {  
    return mFinished;  
}
```
  
```java
private void finish(int finishTask) {  
    if (mParent == null) {  
        int resultCode;  
        Intent resultData;  
        synchronized (this) {  
            resultCode = mResultCode;  
            resultData = mResultData;  
        }  
        if (false) Log.v(TAG, "Finishing self: token=" + mToken);  
        try {  
            if (resultData != null) {  
                resultData.prepareToLeaveProcess(this);  
            }  
            if (ActivityManager.getService()  
                    .finishActivity(mToken, resultCode, resultData, finishTask)) {  
                mFinished = true;  
            }  
        } catch (RemoteException e) {  
            // Empty  
        }  
    } else {  
        mParent.finishFromChild(this);  
    }  
    ...
}
```
      
  
> **onDestroy**: The final call you receive before your activity is destroyed. This can happen either because the activity is finishing (someone called finish() on it, or because the system is temporarily destroying this instance of the activity to save space. You can distinguish between these two scenarios with the isFinishing() method.
  
Backpress
```java
E/test: onPause() - isFinishing: true
E/test: onStop() - isFinishing: true
E/test: onDestroy() - isFinishing: true
```
  
Rotation
```java
E/test: onPause() - isFinishing: false
E/test: onStop() - isFinishing: false
E/test: onDestroy() - isFinishing: false
```
  
`isFinishing () == false` 가 Activity 가 꼭 살아있음을 의미하지는 않음.  
1.  사용자가  Activity 를  완전히  닫거나  Activity 에서 finish() 가  호출되어 종료되는  경우  
2.  구성  변경(rotation, multi window .. ) 으로  인해  시스템이  일시적으로  Activity 를  destroy 시키는  경우  
  
위 2가지 상황을 구분하기 위해서  isFinishing() 을 사용할 수 있음



### isDestroyed()
```java
public boolean isDestroyed() {  
    return mDestroyed;  
}
```

```java
final void performDestroy() {  
    mDestroyed = true;  
    mWindow.destroy();  
    mFragments.dispatchDestroy();  
    onDestroy();  
    writeEventLog(LOG_AM_ON_DESTROY_CALLED, "performDestroy");  
    mFragments.doLoaderDestroy();  
    if (mVoiceInteractor != null) {  
        mVoiceInteractor.detachActivity();  
    }  
}
```

> https://developer.android.com/reference/android/app/Activity#isDestroyed()
> Added in API level 17

> **onDestroy**: There are situations where the system will simply kill the activity's hosting process without calling this method (or any others) in it,

시스템에 의해서 종료되는 경우, onDestory() 호출을 보장할 수 없음
그래서 우리는 데이터를 저장하거나, 리소스를 해제할때
onPuase(), onStop(), onSaveInstanceState(Bundle) 의 위치를 사용함

### 예외처리 방식  
```java
  if  (activity ==  null  || activity.isFinishing()  || activity.isDestroyed())  {  
	  return;  
  }
```
위와 같은 방식으로 대부분의 상황을 예외처리 할 수 있으나, 추천하지 않음
상황에  
  
### 결론  
가장 정석적인 방법은 종료 시점에 요청을 취소하는것,   
(필요에 따라 완료 콜백 이후 isCancelled 와 같은 함수로 확인해서 후처리)  

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY1MzkwMjU1MywxNDIzMTc0NzM0LDE4OT
AyMDA3NDIsLTEzMjY1MzczMTUsMTI2MDYwMDc1OSwxODkxODEw
MjYxLDExMjA3NDEyMDcsMjkwOTk4ODA2LDE0NTExMDI2MzMsMT
AyMzI0ODExOCwxNzk0OTUxMjkxLC0xMzUzNDU5NDEsLTYyMjY2
MjE4MCw2MTg2NzkyLC00MzQ0MDMwNTVdfQ==
-->