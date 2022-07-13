
target sdk 31, agp 7.2.1 
-> 

```
java.lang.Throwable: TimeoutException getting properties for device LMG710N34fa250f

at com.android.ddmlib.PropertyFetcher.handleException(PropertyFetcher.java:248)

at com.android.ddmlib.PropertyFetcher.access$500(PropertyFetcher.java:30)

at com.android.ddmlib.PropertyFetcher$1.run(PropertyFetcher.java:211)

Caused by: com.android.ddmlib.TimeoutException

at com.android.ddmlib.AdbHelper.read(AdbHelper.java:1169)

at com.android.ddmlib.AdbHelper.readAdbResponse(AdbHelper.java:317)

at com.android.ddmlib.AdbHelper.executeRemoteCommand(AdbHelper.java:618)

at com.android.ddmlib.AdbHelper.executeRemoteCommand(AdbHelper.java:475)

at com.android.ddmlib.internal.DeviceImpl.executeShellCommand(DeviceImpl.java:706)

at com.android.ddmlib.PropertyFetcher$1.run(PropertyFetcher.java:207)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbODI3MjMyNDBdfQ==
-->