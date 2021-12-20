


### Firebase Config

> https://github.com/firebase/firebase-android-sdk/tree/master/firebase-config

ExecutorService / Runner 에서 
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
eyJoaXN0b3J5IjpbLTExNjM2MjU5NDUsNDQ1NzAxOTVdfQ==
-->