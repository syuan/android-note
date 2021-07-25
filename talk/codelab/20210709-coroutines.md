


## coroutines

[Introduction to coroutines](https://developer.android.com/codelabs/basic-android-kotlin-training-introduction-coroutines)

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

#### coroutine lecture
[https://www.youtube.com/watch?v=14AGUuh8Bp8&list=PLbJr8hAHHCP5N6Lsot8SAnC28SoxwAU5A&index=2](https://www.youtube.com/watch?v=14AGUuh8Bp8&list=PLbJr8hAHHCP5N6Lsot8SAnC28SoxwAU5A&index=2)


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
- CoroutineContext -> coroutine 은 CoroutineContext 에서 실행이 됨
- CoroutineContext 은 여러 요소를 가지고 있음, job, dispatcher
- newSingleTreadDispatcher(name)



#### Question
Q. main dispatcher 에서 coroutine 에서 delay() 을 하는데 왜 main thread 가 블럭되지 않을까?
-- block 됨, delay() 인 suspend 함수여서 해당 함수가 정지 상태로 만들고 다른 작업을 수행한것
실제로 무거운 작업을 수행하면 main thread 가 블럭 됨,
main dispatcher 에서 무거운 작업하면 안됨
```kotlin
  delay(5_000)  // 예제가 delay 여서 block 되지 않은것 처럼 보였을뿐
```

아래 경우로 테스트 하면 문제 되는거 확인 가능
```kotlin 
  for (i: Int in 1..Int.MAX_VALUE) {  
	  for (j: Int in 1..Int.MAX_VALUE) {  
	      Log.e("test", "multi: " + i * j)  
      }  
  }
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM5MTM3ODc1MiwtNTY3ODE0NTYxLC04NT
Y2NzY2MzYsLTE4OTUxOTEyMTEsLTE1MDQzMjYxOTIsLTI5Nzcx
NzE4MSwtMTAxODcxMDQxNSwtMTg2NTI4MTY2OCwtNDk3MjM1Mj
M1LC0xODM3ODc1MDk2LDEyMDA0MzI0NF19
-->