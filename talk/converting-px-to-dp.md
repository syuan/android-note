

## Resources.getSystem() vs getResources()

  
> Converting px to dp
> https://stackoverflow.com/questions/4605527/converting-pixels-to-dp?answertab=votes#tab-top
  
  
```kotlin
val Number.dp get() = toFloat() * (Resources.getSystem().displayMetrics.densityDpi.toFloat() /  DisplayMetrics.DENSITY_DEFAULT)

val height = 8.dp
```
편하고 코드가 깔끔하긴 한데  
  
- 과연 Resources.getSystem() 은 시스템 리소스 전용인데 사용해도 될까?
- 
application(context) 에서 density 가 변화해도 변경되지 않는 문제가 있나? / 테스트 해볼까?
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTQ1Mzk5ODMzLDcyMDkzMzc4OV19
-->