


### ANR-WatchDog

> https://github.com/SalomonBrys/ANR-WatchDog

```kotlin
new ANRWatchDog().start(); // ANRWatchDog is Thread.class
```

Application Scope 의 worker thread 를 하나 만들고. 
interval time 간격 마다 UI thread handler 로 message 를 보냄. 
interval time 안에 보낸 message 가 수행되지 않으면 ANR 로 판단. 
  
default interval time 은 5000ms

해당 시점의 main thread StackTrace 를 꺼내는 방법

```kotlin
Thread mainThread = Looper.getMainLooper().getThread();
StackTraceElement[] mainStackTrace = mainThread.getStackTrace();
```

  
#### BlockCanary 와 구현 차이가 있나?
> https://github.com/seiginonakama/BlockCanaryEx 




<!--stackedit_data:
eyJoaXN0b3J5IjpbMjk2MjYwOTYsLTg1MjMxNDc1NCwzNjU3Nz
M0MjEsLTIxMjg1NjUzODksMjEzOTM4Nzc3MV19
-->