


## Coroutines and Room

> https://developer.android.com/codelabs/kotlin-android-training-coroutines-and-room#10

#### ViewModelFactory 
ViewModel 이 인자가 있어서 더 큰 생명주의 ViewModel 을 위해서 factory 클래스 필요

#### AndroidViewModel
불가피하게 ViewModel 에서 context 사용하는 경우 사용

#### Room dispatcher
Room 에서는 IO dispatcher 를 따로 사용할 필요 없음 내부적으로 thread pool 에서 동작함
> https://stackoverflow.com/questions/62553769/get-data-from-room-db-using-async-await

#### Kotlin init 순서
> https://medium.com/keepsafe-engineering/an-in-depth-look-at-kotlins-initializers-a0420fcbf546

#### suspend 함수 unit test
suspend 함수를 unit test 작성하는 경우 어떻게 해야하지??
runBlocking<Unit> 사용?? x

> https://craigrussell.io/2019/11/unit-testing-coroutine-suspend-functions-using-testcoroutinedispatcher/
```
@ExperimentalCoroutinesApi class  HeavyWorkerTest { @get:Rule var coroutinesTestRule = CoroutineTestRule() @Test fun  useTestCoroutineDispatcherRunBlockingTest() = coroutinesTestRule.testDispatcher.runBlockingTest { val heavyWorker = HeavyWorker(coroutinesTestRule.testDispatcherProvider) val expected = 666666671666  val result = heavyWorker.heavyOperation() assertEquals(expected, result) } }
```
 
HtmlCompat
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMDE5NzQ3ODFdfQ==
-->