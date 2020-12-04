
# RuntimeException: Canvas: trying to draw too large(xxx bytes) bitmap

       Fatal Exception: java.lang.RuntimeException: Canvas: trying to draw too large(310976100bytes) bitmap.
           at android.graphics.RecordingCanvas.throwIfCannotDraw(RecordingCanvas.java:281)
           at android.graphics.BaseRecordingCanvas.drawBitmap(BaseRecordingCanvas.java:91)
           at android.graphics.drawable.BitmapDrawable.draw(BitmapDrawable.java:548)

> https://github.com/bumptech/glide/issues/3489

Glide 를 사용했는데 너무 큰 Bitmap 이 생성되는 문제
기존에 알고 있는 문제랑 비슷한데 원인은 조금 다름

기존의 이슈는 target ImageVIew 의 크기를 wrap_content 를 사용하는 경우 
Glide 가 target ImageView 의 크기로 target size 로 scale down 을 수행하는데 
wrap_content 와 같은 경우 target size 를 재대로 산정하지 못하고 잘못된 큰 크기로 decoding 하는 문제
> 정확한 동작은 분석 아직 해보지 않음, 
> Glide 이 어떤 코드가 문제인지, size 가 얼마나 잘못 되는지

해당 Glide 이슈는 이전과 비슷하지만 근본적인 문제가 있었음
문제가 발생되는 이미지의 크기는 1000 x 10 (px) 정도로 사이즈의 비율이 한쪽으로 치우친 비정상인 이미징에서 발생

안드로이드 기본 DownsampleStrategy은  CenterOutside 로 Bitmap 재사용을 하기 위해서 scale up 을 하고 있었음
> 항상 scale down 할줄 알았는데, ImageView 가 큰 경우 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ4NzgwODQyMV19
-->