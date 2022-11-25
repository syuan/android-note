


## Using Property File for Custom Lint

> https://github.com/uber/AutoDispose/blob/main/static-analysis/autodispose-lint/src/main/kotlin/autodispose2/lint/AutoDisposeDetector.kt

```kotlin
internal  companion  object {
	internal  const  val  PROPERTY_FILE  =  "gradle.properties"
}

var overrideScopes =  false
val props = Properties()  
context.project.propertyFiles.find { it.name == PROPERTY_FILE }?.apply  
{  
   val content = StringReader(context.client.readFile(this).toString())  
   props.load(content)  
   props.getProperty(OVERRIDE_SCOPES)?.toBoolean()?.let {
	   overrideScopes = it
   }
}
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMTczOTM5NjNdfQ==
-->