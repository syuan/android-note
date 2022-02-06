


### Firebase Config

> https://github.com/firebase/firebase-android-sdk/tree/master/firebase-config

ExecutorService / Runnable 에서 timeout 을 이런식으로 구현하는군
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

> https://github.com/firebase/firebase-android-sdk/tree/ac3276ce7d5f5181b1c419731495eb88a98537af/firebase-config/src/main/java/com/google/firebase/remoteconfig/internal

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQzNjU0OTc2Nyw4ODc5NTI1NDYsNDQ1Nz
AxOTVdfQ==
-->