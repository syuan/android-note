
# RuntimeException: Canvas: trying to draw too large(xxx bytes) bitmap

       Fatal Exception: java.lang.RuntimeException: Canvas: trying to draw too large(310976100bytes) bitmap.
           at android.graphics.RecordingCanvas.throwIfCannotDraw(RecordingCanvas.java:281)
           at android.graphics.BaseRecordingCanvas.drawBitmap(BaseRecordingCanvas.java:91)
           at android.graphics.drawable.BitmapDrawable.draw(BitmapDrawable.java:548)

> https://github.com/bumptech/glide/issues/3489

Glide 를 사용했는데 너무 큰 Bitmap 이 생
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU1NDc3ODQ2XX0=
-->