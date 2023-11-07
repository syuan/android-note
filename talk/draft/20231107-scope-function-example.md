

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


<!--stackedit_data:
eyJoaXN0b3J5IjpbMzI2Mjc3MDMyXX0=
-->