


https://notwoods.github.io/mockk-guidebook/docs/mockito-migrate/void/


1.  void  methods mockking 
mockito 의 경우 when 의 void return 이 안됨
mockk 의 경우 every 에서 Unit 을 사용할 수 있음
```kotlin
val mockedFile = mockk<File>()
every { mockedFile.write(any()) } returns Unit
```


MockK doesn’t have any restrictions with these methods, as they return  `Unit`  in Kotlin. As a result, the standard `returns` infix function can be used.
```

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNTA2MTI4NDEsMTk4OTUzODg5NF19
-->