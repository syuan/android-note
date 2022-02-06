


## Using Property File for Custom Lint

> https://github.com/uber/AutoDispose/blob/main/static-analysis/autodispose-lint/src/main/kotlin/autodispose2/lint/AutoDisposeDetector.kt

```kotlin

val props = Properties()  

context.project.propertyFiles.find { it.name == PROPERTY_FILE }?.apply  
{  
   val content = StringReader(context.client.readFile(this).toString())  
   props.load(content)  
   props.getProperty(CUSTOM_SCOPE_KEY)?.let { scopeProperty ->  
  val customScopes = scopeProperty.split(",")  
         .asSequence()  
         .map(String::trim)  
         .filter(String::isNotBlank)  
         .toList()  
      scopes.addAll(customScopes)  
   }  
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMDU4NjE0NzJdfQ==
-->