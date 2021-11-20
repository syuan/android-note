




> https://stackoverflow.com/questions/23610393/odd-behavior-class-type-of-the-object-retuned-by-the-gettext-method-of-textvi

```java
...
android.widget.TextView.setText (TextView.java:4657)

android.widget.TextView.getIterableTextForAccessibility (TextView.java:11118)

android.view.View.onInitializeAccessibilityEventInternal (View.java:5899)

android.view.View.onInitializeAccessibilityEvent (View.java:5871)

android.widget.TextView.onInitializeAccessibilityEvent (TextView.java:9984)

android.view.View.sendAccessibilityEventUncheckedInternal (View.java:5736)

android.view.View.sendAccessibilityEventUnchecked (View.java:5723)

android.view.View.sendAccessibilityEventInternal (View.java:5700)

android.view.View.sendAccessibilityEvent (View.java:5669)

android.widget.TextView.sendAccessibilityEvent (TextView.java:10153)

android.widget.TextView.onSelectionChanged (TextView.java:8818)

android.widget.TextView.spanChange (TextView.java:9098)

android.widget.TextView$ChangeWatcher.onSpanAdded (TextView.java:11549)

android.text.SpannableStringInternal.sendSpanAdded (SpannableStringInternal.java:314)

android.text.SpannableStringInternal.setSpan (SpannableStringInternal.java:138)

android.text.SpannableString.setSpan (SpannableString.java:46)

android.text.SpannableStringInternal.<init> (SpannableStringInternal.java:52)

android.text.SpannableString.<init> (SpannableString.java:30)

android.widget.TextView.removeSuggestionSpans (TextView.java:5013)

android.widget.TextView.setText (TextView.java:4672)

android.widget.TextView.setText (TextView.java:4657)

android.widget.TextView.getIterableTextForAccessibility (TextView.java:11118)

android.view.View.onInitializeAccessibilityEventInternal (View.java:5899)

android.view.View.onInitializeAccessibilityEvent (View.java:5871)

android.widget.TextView.onInitializeAccessibilityEvent (TextView.java:9984)

android.view.View.sendAccessibilityEventUncheckedInternal (View.java:5736)

android.view.View.sendAccessibilityEventUnchecked (View.java:5723)

android.view.View.sendAccessibilityEventInternal (View.java:5700)

android.view.View.sendAccessibilityEvent (View.java:5669)

android.widget.TextView.sendAccessibilityEvent (TextView.java:10153)

android.widget.TextView.onSelectionChanged (TextView.java:8818)

android.widget.TextView.spanChange (TextView.java:9098)

android.widget.TextView$ChangeWatcher.onSpanAdded (TextView.java:11549)

android.text.SpannableStringInternal.sendSpanAdded (SpannableStringInternal.java:314)

android.text.SpannableStringInternal.setSpan (SpannableStringInternal.java:138)

android.text.SpannableString.setSpan (SpannableString.java:46)

android.text.SpannableStringInternal.<init> (SpannableStringInternal.java:52)

android.text.SpannableString.<init> (SpannableString.java:30)

android.widget.TextView.removeSuggestionSpans (TextView.java:5013)

android.widget.TextView.setText (TextView.java:4672)

android.widget.TextView.setText (TextView.java:4657)

android.widget.TextView.setText (TextView.java:4632)

android.widget.TextView.setMovementMethod (TextView.java:2221)

android.widget.TextView.setTextIsSelectable (TextView.java:6133)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc1NzMzMTcyNl19
-->