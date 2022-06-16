



## IllegalStateException("Can not perform this action after onSaveInstanceState")

IllegalStateException(  
        "Can not perform this action after onSaveInstanceState")
을 겪에 되는 이후는 onSaveInstanceState() 이후에 FragmentTransaction.commit() 을 호출하는 경우, 이 경우 개발자가 의도한 동작과 다르게 동작할수 있으므로 명시적으로 exception 을 던짐


onSavedInstanceState() 이후에 FragmentTransaction.commitAllowingStateLoss() 을 호출하게 되면 이후 fragment 상태를 저장한 이후이기 때문에 fragment 상태가 저장되진 않습니다. 
따라서 시스템에 의해서 Activity 가 종료된 이후에 다시 진입해서 Activity 가 복구될때 해당 fragment 를 복구하지 못함

-> 정리하면, onSaveInstanceState() 이후에 commitAllowingStateLoss() 를 사용하여 fragment 를 attach 하게 되면, 시스템에 의해도 화면이 복구되었을대 fragment 가 없는 상태로 보여짐
따라서 상황에 맞게 commit() / commitAllowingStateLoss() 을 사용하는게 맞음 
dialog fragment 와 같이 복구되지 않아도 크리티컬하지 않다면 commitAllowingStateLoss() 을 사용해도 되지만, 


Fragment 에서 isStateSaved() 를 체크한다는 의미는 
onStop(), onSaveInstanceState() 가 불려서 정지 상태가 되었거나 상태를 저장한 이후인지를 확인하는것

 ```java 
public abstract class FragmentManager implements FragmentResultOwner {
	...
	public boolean isStateSaved() {  
		return mStateSaved || mStopped;  
	} 
}
 ```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MTA1MzM1MjgsMTM0Mjc5NDg2NiwtMT
k3ODAyOTAyNiwtMTIwMTYxODkwXX0=
-->