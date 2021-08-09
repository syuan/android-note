


## RequestOptions

options.override(option.width, option.height)
>https://bumptech.github.io/glide/javadocs/430/com/bumptech/glide/request/RequestOptions.html#override-int-int-

glide 의 override option 을 사용한 경우
```java
Glide.with(this)  
	.load(vo.getUrl())  
    .override(toPx(this, vo.getWidth()), toPx(this, vo.getHeight()))
    .into(target);
```

직접 layout params 의 크기를 설정한 경우
```java
ViewGroup.LayoutParams params = target.getLayoutParams();  
params.width = toPx(this, vo.getWidth());  
params.height = toPx(this, vo.getHeight());  
target.setLayoutParams(params);  
  
Glide.with(this)  
	.load(vo.getUrl())  
    .into(target);
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg1OTc4Mjg5NiwtOTA4MjE1MDYwLC01OD
E4OTA4XX0=
-->