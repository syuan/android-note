


## coroutines advance

> https://developer.android.com/codelabs/kotlin-coroutines?hl=da#0

#### summary
- ViewModelScope
- Dispatcher
- Coroutines Test
- Retrofit, Room with Coroutines


#### question

- ViewModelScope 에서 launch 하면 어느 dispatcher?  
-- ViewModelScope 은 기본이 main dispatcher
-- GlobalScope 은 default dispatcher
-- ViewModelScope, LifecycleScope 은 생명주기에 따라 취소됨
-- GlobalScope 은 문제가 application 의 생명주기를 가지며, exception 발생시 전체 영향을 줌
-- https://medium.com/androiddevelopers/coroutines-patterns-for-work-that-shouldnt-be-cancelled-e26c40f142ad

- 어느 dispatcher 인지 확인하는 방법은?
-- Thread.currentThread().name : thread 확인
-- [-Dkotlinx.coroutines.debug in IntelliJ IDEA?](https://stackoverflow.com/questions/53250953/how-to-enable-dkotlinx-coroutines-debug-in-intellij-idea) : coroutine 

- suspend 함수는 무엇?
--   coroutine suspend 함수는 thread 를 block 하지 않음
--   하나의 thread 에서 여러 개의 coroutine 을 실행, 특정 작업이 suspend 되고 resume 될 때까지 이 사이에 다른 작업을 수행
--   그래서 suspend 는 많은 concurrent 작업을 지원하면서 blocking 에 대한 메모리를 절약

- test rule 2개 무엇?

- CompletableDeferred ?
-- https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines/-completable-deferred/


- SupervisorJob?
--   [SupervisorJob](https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines/-supervisor-job.html)  : Exception을 상위 parent에게 통지하지 않는다. 결국 child 들에서 발생한 Exception이 다른 child에 영향을 주지 않는다.
--   [CoroutineExceptionHandler](https://kotlinlang.org/docs/reference/coroutines/exception-handling.html)  : Exception을 받아 처리한다.

ApplicationScope 을 만드는 경우,
```kotlin
class MyApplication : Application() {  

// No need to cancel this scope as it'll be torn down with the process  
val applicationScope = CoroutineScope(exceptionHandler + SupervisorJob() + otherConfig)

}

val exceptionHandler = CoroutineExceptionHandler { coroutineContext, throwable ->
  // handle exception
}
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA0NDk2MzA4OSwtMjEwMjczNTYyMiwyMT
IzMTA3Mjg2LDEwODIyNDE5MjAsMTgwNjA2Nzc2MywtMTY1NjA3
MTA2MCw4NzcyMTUzMjgsMTg2NTA3NTg5LC0xMDY0Mzc5OTEwXX
0=
-->