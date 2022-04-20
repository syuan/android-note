




```java
private void writeApplicationExitInfoEventIfRelevant(String sessionId) {  
   if (android.os.Build.VERSION.SDK_INT >= Build.VERSION_CODES.R) {  
      ActivityManager activityManager = (ActivityManager) context.getSystemService(Context.ACTIVITY_SERVICE);  
  
  // Gets all the available app exit infos.  
  List<ApplicationExitInfo> applicationExitInfoList =  
            activityManager.getHistoricalProcessExitReasons(null, 0, 0);  
    
  if (applicationExitInfoList.size() != 0) {  
         final LogFileManager relevantSessionLogManager = new LogFileManager(fileStore, sessionId);  
 final UserMetadata relevantUserMetadata =  
               UserMetadata.loadFromExistingSession(sessionId, fileStore, backgroundWorker);  
  reportingCoordinator.persistRelevantAppExitInfoEvent(  
               sessionId, applicationExitInfoList, relevantSessionLogManager, relevantUserMetadata);  
  }  
   }  
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUxOTU2MjE5MV19
-->