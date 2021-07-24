


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
-- GlobalScope 은 사용 자제

- 어느 dispatcher 인지 확인하는 방법은?

- suspend 함수는 무엇?

- test rule 2개 무엇?

- complatableDeferred ?

- SupervisorJob?

> https://medium.com/androiddevelopers/coroutines-patterns-for-work-that-shouldnt-be-cancelled-e26c40f142ad

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgwNjA2Nzc2MywtMTY1NjA3MTA2MCw4Nz
cyMTUzMjgsMTg2NTA3NTg5LC0xMDY0Mzc5OTEwXX0=
-->