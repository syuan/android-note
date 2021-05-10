

# Let non-browser apps handle URLs

> https://developer.android.com/training/package-visibility/use-cases

URI 를 열때 BROWSER 가 아닌 앱들로 제한하고 싶다면 
새로 추가된 FLAG_ACTIVITY_REQUIRE_NON_BROWSER 를 사용하면 됨

해당하는 앱이 없다면 ActivityNotFoundException 이 발생
(URI 를 처리할 수 있는 앱이 BROWSER 들 뿐인 경우도 해당)

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

FLAG_ACTIVITY_REQUIRE_DEFAULT 옵션을 추가하면
UIR 를 처리할 수 있는 앱이 하나가 아닌 복수개여서 CHOOSER 가 나타나는 경우
ActivityNotFoundException 발생 

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
eyJoaXN0b3J5IjpbLTIwMzU3NzE5NjNdfQ==
-->