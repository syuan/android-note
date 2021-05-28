

```java
AccessibilityManager am = (AccessibilityManager) getSystemService(Context.ACCESSIBILITY_SERVICE);

List<AccessibilityServiceInfo> enabledServices = am.getEnabledAccessibilityServiceList(AccessibilityServiceInfo.FEEDBACK_SPOKEN);
boolean isAccessibilityEnabled = am.isEnabled();
 ```
 
```java
boolean accessibilityEnabled = Settings.Secure.getInt(this.getContentResolver(), Settings.Secure.ACCESSIBILITY_ENABLED) == 1
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY1MjQyMzY3OV19
-->