

## How does firebase sdk get ANR events?


> https://github.com/firebase/firebase-android-sdk/blob/5f7ac459817e30f36c0ff9711f00c4011a0ee683/firebase-crashlytics/src/main/java/com/google/firebase/crashlytics/internal/common/CrashlyticsController.java#L809


API 30  ActivityManager.getHistoricalProcessExitReasons
> https://developer.android.com/reference/kotlin/android/app/ActivityManager#getHistoricalProcessExitReasons(kotlin.String,%20kotlin.Int,%20kotlin.Int)

getHistoricalProcessExitReasons 으로 종료 이유 들을 가져옴

```java
private void writeApplicationExitInfoEventIfRelevant(String sessionId) {  
	if (android.os.Build.VERSION.SDK_INT >= Build.VERSION_CODES.R) {  
		ActivityManager activityManager = 
			(ActivityManager) context.getSystemService(Context.ACTIVITY_SERVICE);  
  
		// Gets all the available app exit infos.  
		List<ApplicationExitInfo> applicationExitInfoList =  
            activityManager.getHistoricalProcessExitReasons(null, 0, 0);  
    
		if (applicationExitInfoList.size() != 0) {  
	        final LogFileManager relevantSessionLogManager = 
		        new LogFileManager(fileStore, sessionId);  
			
			final UserMetadata relevantUserMetadata = 
				UserMetadata.loadFromExistingSession(sessionId, fileStore, backgroundWorker);  
			
			reportingCoordinator.persistRelevantAppExitInfoEvent(
				sessionId, 
				applicationExitInfoList, 
				relevantSessionLogManager, r
				elevantUserMetadata);  
		}  
	}  
}
```

종료된 이유 중에 session start 이후의 것 중에 ANR로 종료된 것을 반환

```java
@RequiresApi(api = Build.VERSION_CODES.R)  
private ApplicationExitInfo findRelevantApplicationExitInfo(  
	String sessionId, 
	List<ApplicationExitInfo> applicationExitInfoList) {  

	long sessionStartTime = reportPersistence.getStartTimestampMillis(sessionId);  
	for (ApplicationExitInfo applicationExitInfo : applicationExitInfoList) {  
		if (applicationExitInfo.getTimestamp() < sessionStartTime) {  
	        return null;  
		}  
        
		if (applicationExitInfo.getReason() != ApplicationExitInfo.REASON_ANR) {  
			continue;  
		}  
		return applicationExitInfo;  
	
	}  
	return null;  
}
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIwMDkzNzE3NCwyMTA0ODI1NjA3XX0=
-->