

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
4. decoding 할때 BitmapOption 이 일반적이지 않나?
  
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
  
정상적인 경우와 실패한 경우 bitmap 의 px byte 는 동일했음
Glide 어느 과정에서 chunk 가 손실되거나 만들지 않는것 같음


#### 3. 

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
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {  
   decodeBitmapOptions.inPreferredColorSpace = null;  
   decodeBitmapOptions.outColorSpace = null;  
   decodeBitmapOptions.outConfig = null;  
}  
decodeBitmapOptions.outWidth = 213;  
decodeBitmapOptions.outHeight = 60;  
decodeBitmapOptions.outMimeType = "image/png";  
decodeBitmapOptions.inBitmap = null;  // <-
decodeBitmapOptions.inMutable = false;  
  
LruArrayPool byteArrayPool = new LruArrayPool(4 * 1024 * 1024);  
byte[] bytesForOptions = byteArrayPool.get(ArrayPool.STANDARD_BUFFER_SIZE_BYTES, byte[].class);  
decodeBitmapOptions.inTempStorage = bytesForOptions;
```








> Difference DiskCacheStrategy in Glide v4
https://stackoverflow.com/questions/46349657/difference-diskcachestrategy-in-glide-v4

>  Library which allows you to create a chunk for NinePatchDrawable at runtime
> https://github.com/Anatolii/NinePatchChunk
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkzOTY0Mzg2MCwyMDMyNjg0MTYxLDQyND
kyMjI3XX0=
-->