





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

onSaveInstanceState


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM0Mjc5NDg2NiwtMTk3ODAyOTAyNiwtMT
IwMTYxODkwXX0=
-->