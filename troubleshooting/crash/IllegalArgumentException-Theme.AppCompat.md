





### java.lang.IllegalArgumentException: The style on this component requires your app theme to be Theme.AppCompat (or a descendant). 

Compat Theme 이 아닌곳에서 CoodinatorLayout 을 사용하는 경우 문제

```kotlin
CoordinatorLayout(
	ContextThemeWrapper(
		binding.snackBarContainer.context,
		com.google.android.material.R.style.Theme_AppCompat
	)
)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDc2NDI3Ml19
-->