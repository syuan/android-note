

# Let non-browser apps handle URLs


```kotlin
try {  
  val intent = Intent(ACTION_VIEW, Uri.parse(url)).apply {  
  // The URL should either launch directly in a non-browser app 
  // (if it's the default), or in the disambiguation dialog.  
  addCategory(CATEGORY_BROWSABLE)  
  flags = FLAG_ACTIVITY_NEW_TASK or FLAG_ACTIVITY_REQUIRE_NON_BROWSER  
  }  
  startActivity(intent)  
} catch (e: ActivityNotFoundException) {  
  // Only browser apps are available, or a browser is the default.  
  // So you can open the URL directly in your app, for example in a 
  // Custom Tab.  
  openInCustomTabs(url)  
}
```


```kotlin
try {  
  val intent = Intent(ACTION_VIEW, Uri.parse(url)).apply {  
  // The URL should either launch directly in a non-browser app 
  // (if it's the default), or in the disambiguation dialog.  
  addCategory(CATEGORY_BROWSABLE)  
  flags = FLAG_ACTIVITY_NEW_TASK
   or FLAG_ACTIVITY_REQUIRE_NON_BROWSER  
   or FLAG_ACTIVITY_REQUIRE_DEFAULT
  }  
  startActivity(intent)  
} catch (e: ActivityNotFoundException) {  
  // Only browser apps are available, or a browser is the default.  
  // So you can open the URL directly in your app, for example in a 
  // Custom Tab.  
  openInCustomTabs(url)  
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEzNDE1MzQ0NV19
-->