


### AwDataDirLock

```java
Fatal Exception: io.reactivex.exceptions.OnErrorNotImplementedException: The exception was not handled due to missing onError handler in the subscribe() method call. Further reading: [https://github.com/ReactiveX/RxJava/wiki/Error-Handling](https://github.com/ReactiveX/RxJava/wiki/Error-Handling) | java.lang.RuntimeException: Using WebView from more than one process at once with the same data directory is not supported. [https://crbug.com/558377](https://crbug.com/558377) 
```

webview_data.lock 파일이 문제가 되는 경우 삭제 하는 방식

```java
val file = File(applicationContext.getDir("webview", Context.MODE_PRIVATE).absolutePath + File.separator + "webview_data.lock")  
if (file.exists()) {  
    file.delete()  
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMzc5MTYyMTMsMTYxMDE0MTk2OV19
-->