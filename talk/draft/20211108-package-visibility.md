


## Package Visibility


Types of apps that are visible automatically

([https://developer.android.com/training/package-visibility/automatic](https://developer.android.com/training/package-visibility/automatic))

-   Your own app.
-   [Certain system packages](https://developer.android.com/training/package-visibility/automatic#system-packages-visible-automatically), such as the media provider, that implement core Android functionality.
-   The app that installed your app.
-   Any app that launches an activity in your app using the [`startActivityForResult()`](https://developer.android.com/reference/kotlin/android/app/Activity#startactivityforresult) method, as described in the guide about how to [get a result from an activity](https://developer.android.com/training/basics/intents/result).
-   Any app that starts or binds to a [service](https://developer.android.com/guide/components/services) in your app.
-   Any app that accesses a [content provider](https://developer.android.com/guide/topics/providers/content-providers) in your app.
-   Any app that has a content provider, where your app has been [granted URI permissions](https://developer.android.com/guide/topics/providers/content-provider-basics#getting-access-with-temporary-permissions) to access that content provider.
-   Any app that receives input from your app. This case applies only when your app provides input as an [input method editor](https://developer.android.com/guide/topics/text/creating-input-method).
-   Some system packages that implement core Android functionality are automatically visible to your app, even when your app targets Android 11 or higher.

  
>In addition, you can start another app's activity using either an [implicit](https://developer.android.com/guide/components/intents-filters#ExampleSend) or [explicit](https://developer.android.com/guide/components/intents-filters#ExampleExplicit) intent, regardless of whether that other app is visible to your app.



#### Test
-   제대로 구성한 암시적/명시적 intent 는 startActivity 에 문제가 없다.
-   startActivityForResult() 와 같은 형태에서 callee 는 caller 에 접근할수 있다. (queries 에 선언하지 않아도)
-   action 을 사용하는 경우, 요청하는 spec 에 맞게 queies 를 작성해야한다. (mimeType 포함할것)

#### Issue
intent scheme (불안전한 intent scheme, host 제대로 되어 있지 않은) 을
Intent.class 객체로 매핑해서 startActivity 하는 경우 (package name 만 유효한 경우),
-   30 이전에는 문제가 없었으나,
-   30 부터는 문제가 발생함, 그래서 quieres 에 해당 package 를 추가해서 launch activity 를 가져와서 startActivity 하는 방식으로 처리


#### MediaStore.Images.Media.EXTERNAL_CONTENT_URI

```java
Intent intent = new Intent(Intent.ACTION_PICK, MediaStore.Images.Media.EXTERNAL_CONTENT_URI);
```
content provider 를 나타내는 content:// 라서 mime type 을 
vnd.android.cursor.dir/* 와 같이 해야하나?

> http://egloos.zum.com/shadowxx/v/10462983
> https://stackoverflow.com/questions/64645305/how-to-create-intent-to-choose-image-from-gallery-in-android-11
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTA4MjMyOTBdfQ==
-->