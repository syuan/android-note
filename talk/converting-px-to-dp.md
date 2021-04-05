

## Resources.getSystem() vs getResources()

  
> Converting px to dp
> https://stackoverflow.com/questions/4605527/converting-pixels-to-dp?answertab=votes#tab-top
  
  
```kotlin
val Number.dp get() = toFloat() * (Resources.getSystem().displayMetrics.densityDpi.toFloat() /  DisplayMetrics.DENSITY_DEFAULT)

val height = 8.dp
```
편하고 코드가 깔끔하긴 한데... 
  
- Resources.getSystem() 은 시스템 리소스 전용인데 사용해도 될까?
- ApplicationContext, ActivityContext 가 시스템과 다른 density 를 가지는 경우가 있을까?
- Activity? Application? 이 동적으로 density 변화가 가능한가?
  
  
#### Density 변경 방법



#### Resources.getSystem() 사용이 문제가 되는 경우

App  리소스에 접근하는 경우
```kotlin
getResources().getString(R.string.app_name) // ok
Resources.getSystem().getString(R.string.app_name) // exception
```

시스템 리소스에 접근하는 경우
```kotlin
getResources().getString(android.R.string.cancel) // ok
Resources.getSystem().getString(android.R.string.cancel) // ok
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMjM3ODEwMDIsNTQ5NTY3NDM0LDUxNz
Q5NDk4Miw3MjA5MzM3ODldfQ==
-->