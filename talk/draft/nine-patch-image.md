

## How to resolve nine-patch image from Internet with Glide 4.x 


> https://github.com/bumptech/glide/issues/3555

Glide 4.x 에서 nine patch 이미지를 로드하면 nine patch 가 정상적으로 동작하지 않음
"http://image7.coupangcdn.com/image/mobile_app/v3/badges/preorder/android/xxhdpi/preorder_badge.9.png"
```java
Glide.with(this)  
      .load(url)  
      .into(view);
```

      
아래와 같이 glide 를 통해서 bitmap 객체를 가져오면 nine patch chunk 가 null 임
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


https://www.programmersought.com/article/97346007070/
<- BitmapFactory.decodeFile 사용하는건데 잘 되나 ?





https://github.com/bumptech/glide/issues/1766

https://github.com/Anatolii/NinePatchChunk
<- 라이브러리?




#### Use code to load NinePatch pictures in Android




> Difference DiskCacheStrategy in Glide v4
https://stackoverflow.com/questions/46349657/difference-diskcachestrategy-in-glide-v4

<!--stackedit_data:
eyJoaXN0b3J5IjpbNTk0MDM1MTA3LDU4Njk4NTQ2NSwtNjMyNj
M5ODQxLDE5MjM2NzUzODcsLTYyNDE4MDQ2MiwxODkzNTMxNTNd
fQ==
-->