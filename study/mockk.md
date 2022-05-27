


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

#### 2. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ2MzQzMTI0LDE5ODk1Mzg4OTRdfQ==
-->