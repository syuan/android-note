

# RuntimeException: Canvas: trying to draw too large(xxx bytes) bitmap


```java
Fatal Exception: java.lang.RuntimeException: Canvas: trying to draw too large(120472576bytes) bitmap.
       at android.view.DisplayListCanvas.throwIfCannotDraw(DisplayListCanvas.java:229)
       at android.view.RecordingCanvas.drawBitmap(RecordingCanvas.java:101)
       at android.graphics.drawable.BitmapDrawable.draw(BitmapDrawable.java:545)
       at android.widget.ImageView.onDraw(ImageView.java:1342)
       ...
```

기존에 발생했던 문제와 원인은 비슷하나 발생 조건이 다름. 
  
이 문제는 삼성 galaxy s8~ note8 정도의 단말기에서 OS 9.0 에서만 발생함.   
그리고 시스템 설정에서 해상도를 WQHD+ (최대로) 맞춘 경우에만 발생. 
  
문제의 원인은 기존과 비슷하게 Glide 를 사용할때  match_parent, wrap_content 로 ImageView 의 layout 이 설정되어 있었고 (target size 가 device 로 크기로 설정됨)

이미지의 비율은 (정상적) 1344 x 288
디바이스 비율은 1080 x 2076

Glide 내부 동작으로 CenterOutside(up scale)이 수행되면서 
scale factor 가 7.6 정도 였음

1344 x 288 x 7.6 x 4 로 11766988.8 byte = 11mb 정도 였음
하지만 실제는 120472576bytes 로 decoding 되는 문제가 존재

해당 단말기의 조건에서  크게 디코딩되는 문제가 있었음 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYyOTkxMzg4OV19
-->