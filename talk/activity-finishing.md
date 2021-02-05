
# Activity.isFinishing

> https://github.com/bumptech/glide/issues/1126  

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
일시적인 소멸 시점에는 false 를 반환함.  

onDestroy() 는  활동이  소멸되기  전에  호출, 시스템은  다음  중  하나에 시점에 onDestory() 를 호출

1.  사용자가  Activity를  완전히  닫거나  Activity 에서 finish()가  호출되어 종료되는  경우
2.  구성  변경(예: 기기  회전  또는  멀티  윈도우  모드)으로  인해  시스템이  일시적으로  활동을  소멸시키는  경우
  
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
  
### 결론  
가장 정석적인 방법은 종료 시점에 요청을 취소하는것,   
(추가로, 완료 콜백 이후 isCancelled 와 같은 것으로 확인해서 후처리)  

아래와 같은 callback 에서는 cancel 호출시 onCancel() 만 호출됨
```java
public interface ResponseCallback<T> {

	_/* Runs on the UI thread */_
	void onStart(HttpRequest request);

	_/* Runs on the UI thread */_
	void onFinish();

	_/* Runs on the UI thread */_
	void onResponse(@Nullable T response);

	_/* Runs on the UI thread */_
	void onError(HttpNetworkError error);

	_/* Runs on the UI thread */_
	void onCancel();

	_/* Runs on a worker thread */_
	void onParse(int code, Map<String, String> header, byte[] data, long networkTime, HttpRequestVO httpRequestVO);

	_/* Runs on Worker Thread */_
	void onParseFinished(T object);
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MDY2NjI2OSwxODkxODEwMjYxLDExMj
A3NDEyMDcsMjkwOTk4ODA2LDE0NTExMDI2MzMsMTAyMzI0ODEx
OCwxNzk0OTUxMjkxLC0xMzUzNDU5NDEsLTYyMjY2MjE4MCw2MT
g2NzkyLC00MzQ0MDMwNTVdfQ==
-->