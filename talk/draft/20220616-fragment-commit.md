



## IllegalStateException("Can not perform this action after onSaveInstanceState")

IllegalStateException(  
        "Can not perform this action after onSaveInstanceState")
을 겪에 되는 이후는 onSaveInstanceState() 이후에 FragmentTransaction.commit() 을 호출하는 경우, 이 경우 개발자가 의도한 동작과 다르게 동작할수 있으므로 명시적으로 exception 을 던짐


onSavedInstanceState() 이후에 FragmentTransaction.commitAllowingStateLoss() 을 호출하게 되면 이후 fragment 상태를 저장한 이후이기 때문에 fragment 상태가 저장되진 않습니다. 
따라서 시스템에 의해서 Activity 가 종료된 이후에 다시 진입해서 Activity 가 복구될때 해당 fragment 를 복구하지 못함

정리하면, 



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
eyJoaXN0b3J5IjpbLTU0MjUxMDA0LDEzNDI3OTQ4NjYsLTE5Nz
gwMjkwMjYsLTEyMDE2MTg5MF19
-->