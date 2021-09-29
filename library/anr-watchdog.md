


### ANR-WatchDog

> https://github.com/SalomonBrys/ANR-WatchDog

```kotlin
new ANRWatchDog().start();
// NARWatchDog 
```


Application Scope 의 worker thread 를 하나 만들고. 
interval time 간격 마다 UI thread handler 로 message 를 보냄. 
interval time 안에 보낸 message 가 수행되지 않으면 ANR 로 판단. 
  
default interval time 은 5000ms



#### BlockCanary 와 구현 차이가 있나?
> https://github.com/seiginonakama/BlockCanaryEx 




<!--stackedit_data:
eyJoaXN0b3J5IjpbOTA2ODQyNTcwLDM2NTc3MzQyMSwtMjEyOD
U2NTM4OSwyMTM5Mzg3NzcxXX0=
-->