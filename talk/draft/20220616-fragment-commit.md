



# IllegalStateException("Can not perform this action after onSaveInstanceState")

### Cause
IllegalStateException(  
        "Can not perform this action after onSaveInstanceState")
을 겪에 되는 이유는 onSaveInstanceState() 이후에 FragmentTransaction.commit() 을 호출하는 경우, 이 경우 개발자가 의도한 동작과 다르게 동작할수 있으므로 시스템에서 명시적으로exception 을 던짐

### FragmentTransaction.commitAllowingStateLoss()

onSavedInstanceState() 이후에 FragmentTransaction.commitAllowingStateLoss() 을 호출하게 되면 이후 fragment 상태를 저장한 이후이기 때문에 fragment 마지막 상태가 저장되진 않음 
따라서 시스템에 의해서 Activity 가 종료된 이후에 다시 진입해서 Activity 가 복구될때 해당 fragment 를 복구하지 못함 (fragment add 동작이였다면 이 add 상태도 저장 안됨)

<pre>
정리하면, onSaveInstanceState() 이후에 commitAllowingStateLoss() 를 사용하여 fragment 를 attach 하게 되면, 시스템에 의해도 화면이 복구되었을대 fragment 가 없는 상태로 보여짐
따라서 상황에 맞게 commit() / commitAllowingStateLoss() 을 사용하는게 맞음 
dialog fragment 와 같이 복구되지 않아도 크리티컬하지 않다면 commitAllowingStateLoss() 을 사용해도 되지만, 일반적인 경우에 UI bug 가 될수 있음
</pre>

### FragmentManager.isStateSaved()
Fragment 에서 isStateSaved() 를 체크한다는 의미는 
onStop(), onSaveInstanceState() 가 불려서 정지 상태가 되었거나 상태를 저장한 이후인지를 확인하는것
(OS 버전 마다 다른데, onStop() 이후에 onSaveInstanceState() 호출 됨)
 ```java 
public abstract class FragmentManager implements FragmentResultOwner {
	...
	public boolean isStateSaved() {  
		return mStateSaved || mStopped;  
	} 
}
 ```


### Conclusion
올바른 구현은 LiveData 를 사용해서 onStop() 이후의 상태 변화는 hold하고 onResume() ? 이후 다시 변화가 관찰되도록 구현해야할것 같음
fragment dialog 와 같이 상태를 잃어버려도 된다면 commitAllowingStateLoss() 사용해도 됨.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNjE4MjI3OTYsMTE3OTgzOTkxNSwxMz
EyNDAwNDI0LC0yMDIwNTA5OTQ4LDEzNDI3OTQ4NjYsLTE5Nzgw
MjkwMjYsLTEyMDE2MTg5MF19
-->