

## How to resolve nine-patch image from Internet with Glide 4.x 


> https://github.com/bumptech/glide/issues/3555


아래와 같이 
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
eyJoaXN0b3J5IjpbMTA4MDQ0MTgyNywtNjMyNjM5ODQxLDE5Mj
M2NzUzODcsLTYyNDE4MDQ2MiwxODkzNTMxNTNdfQ==
-->