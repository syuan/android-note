

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

**StickHeaderItemDecoration.class**

```java
public class StickHeaderItemDecoration extends RecyclerView.ItemDecoration {  
  
   private StickyHeaderInterface mListener;  
   private int mStickyHeaderHeight;  
  
   public StickHeaderItemDecoration(@NonNull StickyHeaderInterface listener) {  
      // adapter 의 정보를 접근하기 위한 interface  
  mListener = listener;  
   }  
  
   @Override  
  public void onDrawOver(Canvas c, RecyclerView parent, RecyclerView.State state) {  
      super.onDrawOver(c, parent, state);  
  
      // 현재 RecyclerView 에 보여지는 첫번째 View 반환  
  View topChild = parent.getChildAt(0);  
      if (topChild == null) {  
         return;  
      }  
  
      // 첫번째 보여지는 뷰의 실제 position 을 가져옴  
  int topChildPosition = parent.getChildAdapterPosition(topChild);  
      if (topChildPosition == RecyclerView.NO_POSITION) {  
         return;  
      }  
  
      // 가장 최근의 StickyHeader 를 지원하는 item 의 position 을 가져옴  
  int headerPos = mListener.getHeaderPositionForItem(topChildPosition);  
  
      // StickyHeader 를 그리기 위해서 header item 에 해당하는 뷰를 생성  
  View currentHeader = getHeaderViewForItem(headerPos, parent);  
      // 생성한 뷰의 measure, layout -> 부모에 attach 된 뷰가 아니기 때문에 직접 호출  
  fixLayoutSize(parent, currentHeader);  
  
      // 후보 뷰가 존재한다면 가져옴  
  int contactPoint = currentHeader.getBottom();  
      View childInContact = getChildInContact(parent, contactPoint, headerPos);  
  
      // 다음 후보의 StickyHeader 와 겹치지는 경우  
  if (childInContact != null && mListener.isHeader(parent.getChildAdapterPosition(childInContact))) {  
         moveHeader(c, currentHeader, childInContact);  
         return;  
      }  
  
      // 다음 후보의 StickyHeader 와 겹치지 않는 경우  
  drawHeader(c, currentHeader);  
   }  
  
   ...  
}
```

현재 첫번째 아이템을 기준으로 가장 최근의 StickyHeader 를 지원하는 (isHeader) item 의 position 을 가져옴
```java
public int getHeaderPositionForItem(int itemPosition) {  
   int headerPosition = 0;  
   do {  
      if (this.isHeader(itemPosition)) {  
         headerPosition = itemPosition;  
         break;  
      }  
      itemPosition -= 1;  
   } while (itemPosition >= 0);  
   return headerPosition;  
}
```

RecyclerView interface 를 통해서 해당 item (ViewHolder)의 layout id 를 가져와서 동일한 뷰를 생성
```java
private View getHeaderViewForItem(int headerPosition, RecyclerView parent) {  
   // ViewHolder 또는 item 이 자신의 뷰에 해당하는 layout id 를 제공해줘야함  
  int layoutResId = mListener.getHeaderLayout(headerPosition);  
   View header = LayoutInflater.from(parent.getContext()).inflate(layoutResId, parent, false);  
  
   // 필요에 따라 생성한 뷰에 item 을 binding  
  mListener.bindHeaderData(header, headerPosition);  
   return header;  
}
```

생성한 뷰에 대한 measure, layout 수행
```java
private void fixLayoutSize(ViewGroup parent, View view) {  
  
   // Specs for parent (RecyclerView)  
  int widthSpec = View.MeasureSpec.makeMeasureSpec(parent.getWidth(), View.MeasureSpec.EXACTLY);  
   int heightSpec = View.MeasureSpec.makeMeasureSpec(parent.getHeight(), View.MeasureSpec.UNSPECIFIED);  
  
   // Specs for children (headers)  
  int childWidthSpec = ViewGroup.getChildMeasureSpec(widthSpec, parent.getPaddingLeft() + parent.getPaddingRight(), view.getLayoutParams().width);  
   int childHeightSpec = ViewGroup.getChildMeasureSpec(heightSpec, parent.getPaddingTop() + parent.getPaddingBottom(), view.getLayoutParams().height);  
  
   view.measure(childWidthSpec, childHeightSpec);  
  
   view.layout(0, 0, view.getMeasuredWidth(), mStickyHeaderHeight = view.getMeasuredHeight());  
}
```

후보 뷰가 중첩되는 경우 후보 뷰를 반환
```java
private View getChildInContact(RecyclerView parent, int contactPoint, int currentHeaderPos) {  
   View childInContact = null;  
   for (int i = 0; i < parent.getChildCount(); i++) {  
      int heightTolerance = 0;  
      View child = parent.getChildAt(i);  
  
      if (currentHeaderPos != i) {  
         boolean isChildHeader = mListener.isHeader(parent.getChildAdapterPosition(child));  
         if (isChildHeader) {  
            heightTolerance = mStickyHeaderHeight - child.getHeight();  
         }  
      }  
  
      int childBottomPosition;  
      if (child.getTop() > 0) {  
         childBottomPosition = child.getBottom() + heightTolerance;  
      } else {  
         childBottomPosition = child.getBottom();  
      }  
  
      if (childBottomPosition > contactPoint) {  
         if (child.getTop() <= contactPoint) {  
            // This child overlaps the contactPoint  
  childInContact = child;  
            break;  
         }  
      }  
   }  
   return childInContact;  
}
```

StickyHeader 를 RecyclerView canvas 에 그려줌
```java
private void drawHeader(Canvas c, View header) {  
   c.save();  
   c.translate(0,  0);  
   header.draw(c);  
   c.restore();  
}  
  
private void moveHeader(Canvas c, View currentHeader, View nextHeader) {  
   c.save();  
   // 후보 뷰가 위로 올라올수록 현재 뷰가 위로 올려서 그림  
  c.translate(0, nextHeader.getTop() - currentHeader.getHeight());  
   currentHeader.draw(c);  
   c.restore();  
}
```

### Click Event on StickyHeader
RecyclerView 에 GestureDetectorCompat 를 연결하여 클릭 이벤트를 사용

```java
final GestureDetectorCompat detector = new GestureDetectorCompat(recyclerView.getContext(), new GestureDetector.SimpleOnGestureListener(){  
  
   @Override  
  public boolean onSingleTapConfirmed(MotionEvent e) {  
      // TODO  
	  return super.onSingleTapConfirmed(e);  
   }  
});  
  
recyclerView.setOnTouchListener(new View.OnTouchListener() {  
   @Override  
  public boolean onTouch(View v, MotionEvent event) {  
      return detector.onTouchEvent(event);  
  }  
});
```

StickyHeader 영역을 클릭한 경우, 클릭 이벤트를 StickyHeader 의 자식뷰에게 전달
```java
@Override  
public boolean onSingleTapConfirmed(MotionEvent e) {  
   if (currentHeader != null) {  
  
      int height = currentHeader.getHeight() - dy;  
      if (e.getY() < height) {  
  
         int x = (int) e.getX();  
         int y = (int) e.getY();  
         y = y - dy;  
  
         if (currentHeader instanceof ViewGroup) {  
            ViewGroup parent = (ViewGroup) currentHeader;  
            for (int i = 0; i < parent.getChildCount(); i++) {  
               View child = parent.getChildAt(i);  
  
               Rect rect = new Rect();  
               rect.left = child.getLeft();  
               rect.top = child.getTop();  
               rect.right = child.getRight();  
               rect.bottom = child.getBottom();  
  
               if (rect.contains(x, y)) {  
                  child.performClick();  
               }  
            }  
         } else {  
            currentHeader.performClick();  
         }  
      }  
   }  
   return super.onSingleTapConfirmed(e);  
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM1Nzk2MDQzNiwtNjU4ODYwNTY4XX0=
-->