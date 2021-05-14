

# RuntimeException: Canvas: trying to draw too large(xxx bytes) bitmap


```java
Fatal Exception: java.lang.RuntimeException: Canvas: trying to draw too large(120472576bytes) bitmap.
       at android.view.DisplayListCanvas.throwIfCannotDraw(DisplayListCanvas.java:229)
       at android.view.RecordingCanvas.drawBitmap(RecordingCanvas.java:101)
       at android.graphics.drawable.BitmapDrawable.draw(BitmapDrawable.java:545)
       at android.widget.ImageView.onDraw(ImageView.java:1342)
       ...
```

기존에 발생했던 문제와 원인은 비슷하나 발생 조건이 다름

이 문제는 삼성 galaxy s8~ note8 정도의 단말기에서 OS 9.0 에서만 발생함
그리고 시스템 설정에서 해상도를 WQHD+ (최대로) 맞춘 경우에만 발생

문제의 원인은 기존과 비슷하게 Glide 를 사용할때  ㅡㅁ
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcyMTcwODg2NV19
-->