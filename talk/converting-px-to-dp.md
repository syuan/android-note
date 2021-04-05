

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
  
1. Go to **Settings** > Select **Display** > **Display size settings**
2. Go to **Settings** > **Developer Options** > Under ‘Drawing’ option tap on **Smallest width.**
  
#### Density 변경에 따른 상태 변화
  
```java
public static int dpToPx(int dp) {  
   return (int) (dp * Resources.getSystem().getDisplayMetrics().density);  
}  
  
public static int dpToPx(Context context, int dp) {  
   return (int) (dp * context.getResources().getDisplayMetrics().density);  
}
```
항상 동일한 값이 반환됨
단말기에서 density 를 변경하면 전체에 반영되므로?
하나의 Application 또는 Activity 가 다른 density 를 가지는 케이스 찾지 못함
  
####   

```java
private static int convertDpToPixel(float dp){  
    return (int) (dp * Resources.getSystem().getDisplayMetrics().density);  
}
```
    
#### Resources.getSystem() 사용이 문제가 되는 경우
> https://stackoverflow.com/questions/8633539/resources-getsystem-vs-getresources
  
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
eyJoaXN0b3J5IjpbMjMwNDM5NDAsLTEwMTgwMDU2MTAsLTE2OT
A4NzAxNjAsLTIxMjM3ODEwMDIsNTQ5NTY3NDM0LDUxNzQ5NDk4
Miw3MjA5MzM3ODldfQ==
-->