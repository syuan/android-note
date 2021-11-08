


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



####
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc3Nzk4MTg3OV19
-->