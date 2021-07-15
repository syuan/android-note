

## How to resolve nine-patch image from Internet with Glide 4.x 


> https://github.com/bumptech/glide/issues/3555

Glide 4.x 에서 nine-patch 이미지를 로드하면 nine-patch 가 정상적으로 동작하지 않음. 
"http://.../image/preorder_badge.9.png".   
```java
Glide.with(this)  
      .load(url)  
      .into(view);
```

//TODO glide 를 통한 nine-patch 로드를 실패한 모습  
      
아래와 같이 glide 를 통해서 bitmap 객체를 가져오면 nine-patch chunk 가 null 임  
```java
SimpleTarget<Bitmap> target = new SimpleTarget<Bitmap>(){
    @Override
    public void onResourceReady(Bitmap bitmap, GlideAnimation< ? super Bitmap > glideAnimation){
        byte[] chunk = bitmap.getNinePatchChunk();
        // Detect 9-patch chunk
        if( chunk == null ){
            // Not a 9-patch image, load as regular bitmap
        } else { // 9-patch compiled image found
            // Do 9-patchy things here
        }
    }
};
```


#### Assumptions
1. download 하면서 file의 byte 의 조작이 있나?  
2. downsampling, transform 등의 후처리를 하면서 chunk가 손실 되는건가?  
3. decoding 할때 BitmapOption 이 일반적이지 않나?  


#### 1. Glide 를 통해서 File 다운로드만 수행한 경우

```java
FutureTarget<File> target = Glide.with(this)  
      .downloadOnly()  
      .load(url)  
      .submit();
````
  
File -> NinePatchDrawable. 
```java
private void loadImage(FutureTarget<File> target) {  
   FileInputStream inputStream = new FileInputStream(target.get());  
   Bitmap bitmap = BitmapFactory.decodeStream(inputStream);  
  
   NinePatchDrawable drawable = createNinePatchDrawable(getResources(), bitmap);  
   ...
}  
  
public static NinePatchDrawable createNinePatchDrawable(Resources res, Bitmap bitmap) {  
   NinePatchDrawable drawable = null;  
   byte[] chunk = bitmap.getNinePatchChunk();  
   if (NinePatch.isNinePatchChunk(chunk)) {  
      Rect padding = readPadding(chunk);  
      drawable = new NinePatchDrawable(res, bitmap, chunk, padding, null);  
   }  
   return drawable;  
}  
  
public static Rect readPadding(byte[] chunk) {  
   Rect rect = new Rect();  
   if (NinePatch.isNinePatchChunk(chunk)) {  
      rect.left = getInt(chunk, 12);  
      rect.right = getInt(chunk, 16);  
      rect.top = getInt(chunk, 20);  
      rect.bottom = getInt(chunk, 24);  
   }  
   return rect;  
}  
  
public static int getInt(byte[] chunk, int from) {  
   int b1 = chunk[from + 0];  
   int b2 = chunk[from + 1];  
   int b3 = chunk[from + 2];  
   int b4 = chunk[from + 3];  
   int i = b1 << 0 | b2 << 8 | b3 << 16 | b4 << 24;  
   return i;  
}
```

Glide 가 File 다운로드만 수행하고, File -> NinePatchDrawable 을 직접 수행한 경우 정상 동작  


#### 2. downsampling, transform 을 disable 한 경우

```java
Glide.with(this)  
      .asBitmap()  
      .load(url)  
      .override(Target.SIZE_ORIGINAL, Target.SIZE_ORIGINAL)  
      .dontAnimate()  
      .dontTransform()  
      .skipMemoryCache(true)  
      .downsample(DownsampleStrategy.NONE)  
      .diskCacheStrategy(DiskCacheStrategy.NONE)  
      .into(view)
```
- memory, disk cache disable  
- transform disable  
- downsample disable  
  
정상적인 경우와 실패한 경우 bitmap 의 px byte 는 동일 했음  
Glide 어느 과정에서 chunk 가 손실되거나 만들지 않는것 같음  


#### 3.  decoding Option 을 변경한 경우

Bitmap 을 생성하는 방식은 일반적임, file byte 크기도 동일  
```java
Bitmpa bitmap = BitmapFactory.decodeStream(dataRewinder.rewindAndGet(), null, options);
```

Glide 에서 설정하는 BitmapFactory.Options 값  
```java
BitmapFactory.Options decodeBitmapOptions = new BitmapFactory.Options();  
decodeBitmapOptions.inTempStorage = null;  
decodeBitmapOptions.inDither = false;  
decodeBitmapOptions.inScaled = true;  
decodeBitmapOptions.inSampleSize = 1;  
decodeBitmapOptions.inPreferredConfig = Bitmap.Config.ARGB_8888;  
decodeBitmapOptions.inJustDecodeBounds = false;  
decodeBitmapOptions.inDensity = 0;  
decodeBitmapOptions.inTargetDensity = 0;   
decodeBitmapOptions.outWidth = 213;  
decodeBitmapOptions.outHeight = 60;  
decodeBitmapOptions.outMimeType = "image/png";  
decodeBitmapOptions.inBitmap = null;
decodeBitmapOptions.inMutable = false;  
  
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {  
   decodeBitmapOptions.inPreferredColorSpace = null;  
   decodeBitmapOptions.outColorSpace = null;  
   decodeBitmapOptions.outConfig = null;  
} 

...
 
LruArrayPool byteArrayPool = new LruArrayPool(4 * 1024 * 1024);  
byte[] bytesForOptions = byteArrayPool.get(ArrayPool.STANDARD_BUFFER_SIZE_BYTES, byte[].class);  
decodeBitmapOptions.inTempStorage = bytesForOptions;
```

> https://stackoverflow.com/a/15840932
> The caller must ensure that that bitmap and padding are not modified after this method returns. We could copy them, but Bitmap.createBitmap(Bitmap) does not copy the nine-patch chunk on some Android versions.

댓글의 코드 주석중에 bitmap 을 복사하는 경우 chunck 가 복사되지 않을 수 있다는것에서 힌트를 얻음  

Options.inBitmap 의 경우 기존 Bitmap 객체를 재사용 하는거니까 문제가 될수도?  
디버깅을 통해서 중간에 Options.inBitmap 값을 null 로 바꿔주면 nine-patch chunk 가 정상적으로 생성되는것을 확인  
  
Glide 내부에서 LruBitmapPool.class 에서 Bitmap 을 꺼내서 inBitmap 옵션으로 넣어줌  
저장된 동일한 size 의 bitmap 이 없는 경우, 동일 크기의 bitmap 을 생성해서 반환    


#### BitmapFactory.Options.inBitmap   

> Android 3.0(API 수준 11)에는 BitmapFactory.Options.inBitmap 필드가 도입되었습니다. 이 옵션을 설정하면 객체를 취하는 디코딩 메서드가 콘텐츠를 로드할 때 기존 비트맵을 재사용하려고 시도합니다. 즉, 비트맵의 메모리를 재사용하여 성능이 향상되고 메모리 할당과 할당 해제가 모두 삭제됩니다. 그러나 inBitmap 사용 방법에는 특정한 제한사항이 있습니다. 특히, Android 4.4(API 수준 19) 이전 버전에서는 동일한 크기의 비트맵만 지원됩니다.
> https://developer.android.com/topic/performance/graphics/manage-memory





> Difference DiskCacheStrategy in Glide v4
https://stackoverflow.com/questions/46349657/difference-diskcachestrategy-in-glide-v4

>  Library which allows you to create a chunk for NinePatchDrawable at runtime
> https://github.com/Anatolii/NinePatchChunk
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAyMjk0MDY2MSwxNTIxNTg2NjY5LDEwMT
Y1NzIwMjksMjQwODk1OTk3LDIwMzI2ODQxNjEsNDI0OTIyMjdd
fQ==
-->