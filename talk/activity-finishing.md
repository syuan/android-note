
# Activity.isFinishing
  
### isFinishing()
  
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


//TODO finish 함수 - isFinishing()
//TODO onDestory 함수 - isDestory() <- version

### isDestroyed()



### 예외처리 방식  
```java
  if  (activity ==  null  || activity.isFinishing()  || activity.isDestroyed())  {  
  return;  
  }
```
  
가장 정석적인 방법은 요청을 취소하는것,   
(완료 콜백 이후 isCancelled 와 같은 것으로 확인)  
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNTM0NTk0MSwtNjIyNjYyMTgwLDYxOD
Y3OTIsLTQzNDQwMzA1NV19
-->