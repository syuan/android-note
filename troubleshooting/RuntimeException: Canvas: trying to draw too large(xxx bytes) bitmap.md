
# RuntimeException: Canvas: trying to draw too large(xxx bytes) bitmap

       Fatal Exception: java.lang.RuntimeException: Canvas: trying to draw too large(310976100bytes) bitmap.
           at android.graphics.RecordingCanvas.throwIfCannotDraw(RecordingCanvas.java:281)
           at android.graphics.BaseRecordingCanvas.drawBitmap(BaseRecordingCanvas.java:91)
           at android.graphics.drawable.BitmapDrawable.draw(BitmapDrawable.java:548)

> https://github.com/bumptech/glide/issues/3489

Glide 를 사용했는데 너무 큰 Bitmap 이 생성되는 문제
기존에 알고 있는 문제랑 비슷한데 원인은 조금 다름

기존의 이슈는 target ImageVIew 의 크기를 wrap_content 를 사용하는 경우 
Glide 가 target ImageVi
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYxNTgzMzg3Nl19
-->