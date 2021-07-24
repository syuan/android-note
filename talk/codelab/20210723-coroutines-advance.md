


## coroutines advance

> https://developer.android.com/codelabs/kotlin-coroutines?hl=da#0

#### summary
- ViewModelScope
- Dispatcher
- Coroutines Test
- Retrofit, Room with Coroutines


#### question

- ViewModelScope 에서 launch 하면 어느 dispatcher?  
-- ViewModelScope.launch 로 생성된 coroutine 은 main dispatcher
-- GlobalScope.lauch 로 생성된 coroutine 은 default dispatcher
-- ViewModelScope, LifecycleScope 은 생명주기에 따라 취소됨
-- GlobalScope 은 문제가 application 의 생명주기를 가지므로 사용 자제
-- https://medium.com/androiddevelopers/coroutines-patterns-for-work-that-shouldnt-be-cancelled-e26c40f142ad

- 어느 dispatcher 인지 확인하는 방법은?

- suspend 함수는 무엇?

- test rule 2개 무엇?

- complatableDeferred ?

- SupervisorJob?
--   [SupervisorJob](https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines/-supervisor-job.html)  : Exception을 상위 parent에게 통지하지 않는다. 결국 child 들에서 발생한 Exception이 다른 child에 영향을 주지 않는다.
--   [CoroutineExceptionHandler](https://kotlinlang.org/docs/reference/coroutines/exception-handling.html)  : Exception을 받아 처리한다.


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMyNjM3NDAwLDE4MDYwNjc3NjMsLTE2NT
YwNzEwNjAsODc3MjE1MzI4LDE4NjUwNzU4OSwtMTA2NDM3OTkx
MF19
-->