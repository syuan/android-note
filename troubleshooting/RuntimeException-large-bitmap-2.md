

# RuntimeException: Canvas: trying to draw too large(xxx bytes) bitmap


```java
Fatal Exception: java.lang.RuntimeException: Canvas: trying to draw too large(120472576bytes) bitmap.
       at android.view.DisplayListCanvas.throwIfCannotDraw(DisplayListCanvas.java:229)
       at android.view.RecordingCanvas.drawBitmap(RecordingCanvas.java:101)
       at android.graphics.drawable.BitmapDrawable.draw(BitmapDrawable.java:545)
       at android.widget.ImageView.onDraw(ImageView.java:1342)
       ...
```

기존에 발생했던 문제와 원인은 비슷하나 발생 조건
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzMwMjg3NDE1XX0=
-->