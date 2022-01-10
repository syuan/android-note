
# IndexOutOfBoundsException: Inconsistency detected. Invalid view holder adapter

```java
Fatal Exception: java.lang.IndexOutOfBoundsException: Inconsistency detected. Invalid view holder adapter positionBundleSetProductViewHolder{b1f9d07 position=2 id=-1, oldPos=2, pLpos:-1 scrap [attachedScrap] tmpDetached no parent} androidx.recyclerview.widget.RecyclerView{251ef53 VFED..... ......I. 0,3-1080,1049 #7f09021f app:id/bundle_set_list}, adapter:com.coupang.mobile.domain.sdp.interstellar.view.BundleSetItemListAdapter@1006090, layout:androidx.recyclerview.widget.LinearLayoutManager@9f52d89, context:com.coupang.mobile.domain.sdp.interstellar.view.NewSdpActivity@33da605
       at androidx.recyclerview.widget.RecyclerView$Recycler.validateViewHolderForOffsetPosition(RecyclerView.java:5974)
       at androidx.recyclerview.widget.RecyclerView$Recycler.tryGetViewHolderForPositionByDeadline(RecyclerView.java:6158)
       at androidx.recyclerview.widget.RecyclerView$Recycler.getViewForPosition(RecyclerView.java:6118)
       at androidx.recyclerview.widget.RecyclerView$Recycler.getViewForPosition(RecyclerView.java:6114)
       at androidx.recyclerview.widget.LinearLayoutManager$LayoutState.next(LinearLayoutManager.java:2303)
       at androidx.recyclerview.widget.LinearLayoutManager.layoutChunk(LinearLayoutManager.java:1627)
       at androidx.recyclerview.widget.LinearLayoutManager.fill(LinearLayoutManager.java:1587)
       at androidx.recyclerview.widget.LinearLayoutManager.onLayoutChildren(LinearLayoutManager.java:665)
       at androidx.recyclerview.widget.RecyclerView.dispatchLayoutStep1(RecyclerView.java:4085)
       at androidx.recyclerview.widget.RecyclerView.onMeasure(RecyclerView.java:3534)
       at android.view.View.measure(View.java:26411)
```


notifyItemRangeChanged(int positionStart, int itemCount)

와 같은 함수에서 범위를 잘못 지정한 경우 exception 발생

<!--stackedit_data:
eyJoaXN0b3J5IjpbMzc0ODQxNjgzXX0=
-->