

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

```

```



https://www.programmersought.com/article/97346007070/
<- BitmapFactory.decodeFile 사용하는건데 잘 되나 ?





https://github.com/bumptech/glide/issues/1766

https://github.com/Anatolii/NinePatchChunk
<- 라이브러리?




#### Use code to load NinePatch pictures in Android




> Difference DiskCacheStrategy in Glide v4
https://stackoverflow.com/questions/46349657/difference-diskcachestrategy-in-glide-v4

<!--stackedit_data:
eyJoaXN0b3J5IjpbOTcyMDU4MzA0LDIwMzI2ODQxNjEsNDI0OT
IyMjddfQ==
-->