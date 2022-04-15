

## Run assertions with an argument


> https://notwoods.github.io/mockk-guidebook/docs/matching/with/

```kotlin
verify {
  network.upload(any())
}
```

```kotlin
val file = File("hello", data = "world".toByteArray())

verify {
  network.upload(file)
}
```


#### withArg

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

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYyMDMzOTY2M119
-->