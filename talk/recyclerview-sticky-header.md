

## Android RecyclerView StickyHeader without external library

StickyHeader 를 만드는 가장 간단한 방법은 floating dummy view 를 만들어서 사용



### Custom ItemDecoration 을 사용한 StickyHeader 
> https://medium.com/@saber.solooki/sticky-header-for-recyclerview-c0eb551c3f68
> https://github.com/saber-solooki/StickyHeader

지나간 item 중에서 sticky header 을 지원하는 item 의 view 를 decoration 으로 그린다.
```java
public abstract static class ItemDecoration {  
  
   public void onDraw(@NonNull Canvas c, @NonNull RecyclerView parent, @NonNull State state) {  
  
   }  
  
   public void onDrawOver(@NonNull Canvas c, @NonNull RecyclerView parent, @NonNull State state) {  
      //TODO  
   }  
  
   public void getItemOffsets(@NonNull Rect outRect, @NonNull View view, @NonNull RecyclerView parent, @NonNull State state) {  
  
   }  
  ...
}
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwOTM1OTU2Ml19
-->