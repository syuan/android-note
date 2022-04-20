

## How does firebase sdk get ANR events?


> https://github.com/firebase/firebase-android-sdk/blob/5f7ac459817e30f36c0ff9711f00c4011a0ee683/firebase-crashlytics/src/main/java/com/google/firebase/crashlytics/internal/common/CrashlyticsController.java#L809

> 

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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMjg4NDAwMl19
-->