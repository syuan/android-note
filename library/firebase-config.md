


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

<!--stackedit_data:
eyJoaXN0b3J5IjpbODg3OTUyNTQ2LDQ0NTcwMTk1XX0=
-->