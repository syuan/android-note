

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
eyJoaXN0b3J5IjpbNDI0OTIyMjddfQ==
-->