

### Apply

```kotlin
open fun createFromFile(  
	  databaseFile: File,  
	  callback: PrepackagedDatabaseCallback  
) = apply {  
	  this.prepackagedDatabaseCallback = callback  
	  this.copyFromFile = databaseFile  
}
```

```kotlin
val intent = Intent().apply {  
	  setDataAndType(request.uri, request.mimeType)  
	  action = request.action  
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYyOTI4NDg1Ml19
-->