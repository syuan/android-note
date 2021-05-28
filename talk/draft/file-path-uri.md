

```java
private static Uri getUriForFile(File file, Context mActivity) {  
   Timber.d("getUriForFile() %s", file);  
   try {  
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N) {  
         return FileProvider.getUriForFile(mActivity, mActivity.getApplicationContext().getPackageName() + ".apkgfileprovider", file);  
      }  
   } catch (Exception e) {  
      // #6628 - What would cause this? Is the fallback is effective? Telemetry to diagnose more:  
  Timber.w(e, "getUriForFile failed on %s - attempting fallback", file);  
   }  
  
   return Uri.fromFile(file);  
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMyODEwNTc5NF19
-->