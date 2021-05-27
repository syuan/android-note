

```java
AccessibilityManager am = (AccessibilityManager) getSystemService(Context.ACCESSIBILITY_SERVICE);

List<AccessibilityServiceInfo> enabledServices = am.getEnabledAccessibilityServiceList(AccessibilityServiceInfo.FEEDBACK_SPOKEN);
boolean isAccessibilityEnabled = am.isEnabled();
 ```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAxMzgzMzUwOF19
-->