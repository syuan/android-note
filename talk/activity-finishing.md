
# Activity.isFinishing
  
### isFinishing()
  
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
일시적인 destory 에는 false 를 반환함.  
예) rotation, (또 뭐가 있을까?)
  
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

### 예외처리 방식  
```java
  if  (activity ==  null  || activity.isFinishing()  || activity.isDestroyed())  {  
  return;  
  }
```
  
### 결론  
가장 정석적인 방법은 종료 시점에 요청을 취소하는것,   
(추가로, 완료 콜백 이후 isCancelled 와 같은 것으로 확인해서 후처리)  
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ1MTEwMjYzMywxMDIzMjQ4MTE4LDE3OT
Q5NTEyOTEsLTEzNTM0NTk0MSwtNjIyNjYyMTgwLDYxODY3OTIs
LTQzNDQwMzA1NV19
-->