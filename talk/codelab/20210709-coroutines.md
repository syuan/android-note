


## coroutines

[Introduction to coroutines](https://developer.android.com/codelabs/basic-android-kotlin-training-introduction-coroutines)

[https://www.youtube.com/watch?v=14AGUuh8Bp8&list=PLbJr8hAHHCP5N6Lsot8SAnC28SoxwAU5A&index=2](https://www.youtube.com/watch?v=14AGUuh8Bp8&list=PLbJr8hAHHCP5N6Lsot8SAnC28SoxwAU5A&index=2)

#### playground
- [https://developer.android.com/training/kotlinplayground](https://developer.android.com/training/kotlinplayground)
- [https://play.kotlinlang.org/](https://play.kotlinlang.org/)


#### summary
- coroutine builder - launch (job), async (deferred), runBlocking
- Job - cancel, join
- Deferred - await
- yield()
- suspend function
- scop - global scope
- Dispatcher

- Scope . {builder function} (coroutine context)


1~2
- 코루틴은 callback 형태의 코드를 순차적인 코드로 바꿔줌
- coroutine 을 만들기 위한 builder ->  launch, aysnc, runBlocking
- suspend function -> suspend, delay(), join()
- structured concurrency -> 부모 coroutine 블럭과 자식 coroutine 블럭 간의 관계를 만들어서 자식이 끝나야 부모가 종료
- coroutine 이 thread 의 사용보다 성능이 좋음
- suspend / resume -> suspend 함수의 경우 일수 중단 할수 있어서 suspend 함수간에 중단, 재개를 반복


3~4
- job cancel 가능
- cancel 이 정상 동작을 위해서는 suspend 함수를 사용하거나, isActive 체크
- cancel 을 위해 delay(1) 대신 yield(), ensureActive()
- withTimeout, withTimeoutOrNull
- main dispatcher 에서 launch 를 사용해도 block 되지 않네, runBlocking 은 블럭 됨
- async
- GlobalScope 을 사용하면 exception 발생시 의도하지 않게 application 종료가 되니
parent, child coroutine 구조의  structured concurrency 구조로 작성해서 exception 발생서 종료가 전파되도록 하는게 좋음

5~6
- CPS (continuation passing style)
- label 로 구간을 나누고, Continuation(state) 를 suspend 함수 마다 전달되고, 계속 반복되는 형태, 
- Continuation 의 label (step) 이 계속 업데이트 되면서 다음 함수를 순차 수행
- suspend 함수의 작업이 끝나면 label 업데이트하고 resume 되면서 다시 switch case 로 이동



#### Question
Q. main dispatcher 에서 coroutine 에서 sleep() 을 하는데 왜 main thread 가 블럭되지 않을까?
-- ddd
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg1NjY3NjYzNiwtMTg5NTE5MTIxMSwtMT
UwNDMyNjE5MiwtMjk3NzE3MTgxLC0xMDE4NzEwNDE1LC0xODY1
MjgxNjY4LC00OTcyMzUyMzUsLTE4Mzc4NzUwOTYsMTIwMDQzMj
Q0XX0=
-->