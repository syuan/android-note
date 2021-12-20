


### Firebase Config

> https://github.com/firebase/firebase-android-sdk/tree/master/firebase-config

```java
CountDownLatch latch =  new  CountDownLatch(1);
latch.await(timeout, unit);

if (!latch.await(timeout, unit)) {

throw new TimeoutException("Task await timed out.");

}

if (task.isSuccessful()) {

return task.getResult();

} else {

throw new ExecutionException(task.getException());

}
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NDQ2MjA1NDQsNDQ1NzAxOTVdfQ==
-->