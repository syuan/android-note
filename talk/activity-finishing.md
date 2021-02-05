
# Activity.isFinishing
  
  
> **onDestroy**: The final call you receive before your activity is destroyed. This can happen either because the activity is finishing (someone called finish() on it, or because the system is temporarily destroying this instance of the activity to save space. You can distinguish between these two scenarios with the isFinishing() method.
  
Backpress
```java
E/test: onPause() - isFinishing: true
E/test: onStop() - isFinishing: true
E/test: onDestroy() - isFinishing: true
```
  
Rotation
```java
E/test: onPause() - isFinishing: false
E/test: onStop() - isFinishing: false
E/test: onDestroy() - isFinishing: false
```
  
`isFinishing () == false` 가 Activity 가 꼭 살아있음을 의미하지는 않음.
일시적인 destory 에는 false 를 반환함 예로 rotation, 또??



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM3Mjc4MDExMyw2MTg2NzkyLC00MzQ0MD
MwNTVdfQ==
-->