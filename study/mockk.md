


https://notwoods.github.io/mockk-guidebook/docs/mockito-migrate/void/


#### 1.  void  methods mockking 
mockito 의 경우 when 의 void return 이 안됨
mockk 의 경우 every 에서 Unit 을 사용할 수 있음
```kotlin
val mockedBitmap = mockk<Bitmap>()
every { mockedBitmap.write(any()) } returns Unit
```
justRun 을 사용할 수도 있음
```kotlin
val mockedBitmap = mockk<Bitmap>()
justRun { mockedBitmap.write(any()) }
```

#### 2. assertions with  argument

mockito 의 ArgumentCaptor 와 같은 방법은 mockk 의 slot()
```kotlin
val network = mockk<FileNetwork>()
val slot = slot<String>()

every { network.download(capture(slot)) } returns mockk()

network.download("testfile")

verify {
  network.download(any())
}
assertTrue("testfile" == slot.captured)
```

withArg() 를 사용해서 argument 체크 
```kotlin
val expected = File("hello", data = "world".toByteArray())

network.upload(File("hello", data = "world".toByteArray()))

verify {
  network.upload(withArg {
    assertTrue(expected.name == it.name)
    assertTrue(expected.data contentEquals it.data)
  })
}
```
참고: withNullableArg() 


#### 3.  custom matching functions

커스텀한 matcher 를 만드는 방법
```kotlin
every {
  mockedCar.drive(match { engine ->
    engine.type === "Diesel"
  })
} returns true
```
참고: matchNullable() 


#### 4. # automatically stub by relaxing
mock 객체에 대해서 mock 하지 함수는 문제가 생기는데 이 경우 전체 함수를 자동으로 mock 하는 경우는 `relaxed` 사용
```kotlin
val navigator = mockk<Navigator>(relaxed = true)
```
Unit 을 반환하는 함수만 mock 하는 경우 `relaxUnitFun` 을 사용할 수 있음
```kotlin
val navigator = mockk<Navigator>(relaxUnitFun = true)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYzNDQ1NzA0LDE3MDU5MDE0NywxNDYzND
MxMjQsMTk4OTUzODg5NF19
-->