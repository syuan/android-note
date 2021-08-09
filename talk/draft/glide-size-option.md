


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

width = 80, height = 20 인 경우,  
into 의 target view 만큼 request size 를 산정하므로 실제 target view 에 할당된 bitmap 의 크기는 동일 
  
첫번째 케이스의 경우, target view 의 size 를 wrap_content 로 두는 경우가 일반적이라 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MjA4ODg4MjUsLTkwODIxNTA2MCwtNT
gxODkwOF19
-->