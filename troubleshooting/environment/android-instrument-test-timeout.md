


##


> https://issuetracker.google.com/issues/223435826
동일한 stack 은 아니나 에러의 내용은 거의 유사
AGP 7.3.0-alpha07 에서 수행하니 해결 된듯



```
com.google.testing.platform.api.plugin.PluginException: Exception thrown during onBeforeAll invocation of plugin com.google.testing.platform.plugin.android.AndroidDevicePlugin.

at com.google.testing.platform.plugin.PluginLifecycleKt.invokeOrThrow(PluginLifecycle.kt:216)

at com.google.testing.platform.plugin.PluginLifecycleKt.invokeOrThrow$default(PluginLifecycle.kt:205)

at com.google.testing.platform.plugin.PluginLifecycle$onBeforeAll$1.invoke(PluginLifecycle.kt:92)

at com.google.testing.platform.plugin.PluginLifecycle$onBeforeAll$1.invoke(PluginLifecycle.kt:88)

at com.google.testing.platform.core.telemetry.common.noop.NoopDiagnosticsScope.recordEvent(NoopDiagnosticsScope.kt:35)

at com.google.testing.platform.core.telemetry.TelemetryKt.recordEvent(Telemetry.kt:105)

at com.google.testing.platform.core.telemetry.TelemetryKt.recordEvent$default(Telemetry.kt:98)

at com.google.testing.platform.plugin.PluginLifecycle.onBeforeAll(PluginLifecycle.kt:88)

at com.google.testing.platform.executor.SingleDeviceExecutor$execute$4.invoke(SingleDeviceExecutor.kt:86)

at com.google.testing.platform.executor.SingleDeviceExecutor$execute$4.invoke(SingleDeviceExecutor.kt:86)

at com.google.testing.platform.executor.SingleDeviceExecutor.runUnlessCancelled(SingleDeviceExecutor.kt:105)

at com.google.testing.platform.executor.SingleDeviceExecutor.execute(SingleDeviceExecutor.kt:86)

at com.google.testing.platform.RunnerImpl.run(RunnerImpl.kt:108)

at com.google.testing.platform.server.strategy.NonInteractiveServerStrategy$run$4.invoke(NonInteractiveServerStrategy.kt:80)

at com.google.testing.platform.server.strategy.NonInteractiveServerStrategy$run$4.invoke(NonInteractiveServerStrategy.kt:79)

at com.google.testing.platform.core.telemetry.common.noop.NoopDiagnosticsScope.recordEvent(NoopDiagnosticsScope.kt:35)

at com.google.testing.platform.core.telemetry.TelemetryKt.recordEvent(Telemetry.kt:66)

at com.google.testing.platform.server.strategy.NonInteractiveServerStrategy.run(NonInteractiveServerStrategy.kt:79)

at com.google.testing.platform.main.MainKt$main$4.invokeSuspend(Main.kt:67)

at kotlin.coroutines.jvm.internal.BaseContinuationImpl.resumeWith(ContinuationImpl.kt:33)

at kotlinx.coroutines.DispatchedTask.run(DispatchedTask.kt:106)

at kotlinx.coroutines.EventLoopImplBase.processNextEvent(EventLoop.common.kt:274)

at kotlinx.coroutines.BlockingCoroutine.joinBlocking(Builders.kt:85)

at kotlinx.coroutines.BuildersKt__BuildersKt.runBlocking(Builders.kt:59)

at kotlinx.coroutines.BuildersKt.runBlocking(Unknown Source)

at kotlinx.coroutines.BuildersKt__BuildersKt.runBlocking$default(Builders.kt:38)

at kotlinx.coroutines.BuildersKt.runBlocking$default(Unknown Source)

at com.google.testing.platform.main.MainKt.main(Main.kt:66)

at com.google.testing.platform.main.MainKt.main$default(Main.kt:34)

at com.google.testing.platform.main.MainKt.main(Main.kt)

at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)

at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)

at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)

at java.base/java.lang.reflect.Method.invoke(Method.java:566)

at com.google.testing.platform.launcher.Launcher.main(Launcher.java:149)

Caused by: kotlinx.coroutines.TimeoutCancellationException: Timed out waiting for 120000 ms

at kotlinx.coroutines.TimeoutKt.TimeoutCancellationException(Timeout.kt:186)

at kotlinx.coroutines.TimeoutCoroutine.run(Timeout.kt:156)

at kotlinx.coroutines.EventLoopImplBase$DelayedRunnableTask.run(EventLoop.common.kt:497)

at kotlinx.coroutines.EventLoopImplBase.processNextEvent(EventLoop.common.kt:274)

at kotlinx.coroutines.DefaultExecutor.run(DefaultExecutor.kt:69)

at java.base/java.lang.Thread.run(Thread.java:834)

  

Jul 12, 2022 9:38:08 PM com.google.testing.platform.server.strategy.NonInteractiveServerStrategy run

INFO: Shutting down runner.
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUyMjg1OTMyOF19
-->