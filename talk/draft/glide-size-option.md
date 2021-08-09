


RequestOptions

options.override(option.width, option.height)
options.override(Target.SIZE_ORIGINAL, Target.SIZE_ORIGINAL)


requestBuilder.submit(option.width, option.height) ??


```java
Glide.with(this)  
	.load(vo.getUrl())  
    .override(toPx(this, vo.getWidth()), toPx(this, vo.getHeight()))
    .into(target);
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzOTE3MzU2ODcsLTkwODIxNTA2MCwtNT
gxODkwOF19
-->