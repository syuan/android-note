


RequestOptions

options.override(option.width, option.height)
options.override(Target.SIZE_ORIGINAL, Target.SIZE_ORIGINAL)


requestBuilder.submit(option.width, option.height) ??


glide 의 override option 을 사용한 경우
```java
Glide.with(this)  
	.load(vo.getUrl())  
    .override(toPx(this, vo.getWidth()), toPx(this, vo.getHeight()))
    .into(target);
```

직접 layout params 의 크기를 설정한 경우
```
ViewGroup.LayoutParams params = target.getLayoutParams();  
params.width = toPx(this, vo.getWidth());  
params.height = toPx(this, vo.getHeight());  
target.setLayoutParams(params);  
  
Glide.with(this)  
	.load(vo.getUrl())  
    .into(target);
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbODA5MzI5NDY5LC05MDgyMTUwNjAsLTU4MT
g5MDhdfQ==
-->