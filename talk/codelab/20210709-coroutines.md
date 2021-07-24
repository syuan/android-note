


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
- 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MDQzMjYxOTIsLTI5NzcxNzE4MSwtMT
AxODcxMDQxNSwtMTg2NTI4MTY2OCwtNDk3MjM1MjM1LC0xODM3
ODc1MDk2LDEyMDA0MzI0NF19
-->