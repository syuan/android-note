



# IllegalStateException("Can not perform this action after onSaveInstanceState")

### Cause
IllegalStateException(  
        "Can not perform this action after onSaveInstanceState")
을 겪에 되는 이유는 onSaveInstanceState() 이후에 FragmentTransaction.commit() 을 호출하는 경우, 이 경우 개발자가 의도한 동작과 다르게 동작할수 있으므로 시스템에서 명시적으로exception 을 던짐

### FragmentTransaction.commitAllowingStateLoss()

onSavedInstanceState() 이후에 FragmentTransaction.commitAllowingStateLoss() 을 호출하게 되면 이후 fragment 상태를 저장한 이후이기 때문에 fragment 마지막 상태가 저장되진 않음 
따라서 시스템에 의해서 Activity 가 종료된 이후에 다시 진입해서 Activity 가 복구될때 해당 fragment 를 복구하지 못함 (fragment add 동작이였다면 이 add 상태도 저장 안됨)

> 정리하면, onSaveInstanceState() 이후에 commitAllowingStateLoss() 를 사용하여 fragment 를 attach 하게 되면, 시스템에 의해도 화면이 복구되었을대 fragment 가 없는 상태로 보여짐
따라서 상황에 맞게 commit() / commitAllowingStateLoss() 을 사용하는게 맞음 
dialog fragment 와 같이 복구되지 않아도 크리티컬하지 않다면 commitAllowingStateLoss() 을 사용해도 되지만, 일반적인 경우에 UI bug 가 될수 있음


### FragmentManager.isStateSaved()
Fragment 에서 isStateSaved() 를 체크한다는 의미는 
onStop(), onSaveInstanceState() 가 불려서 정지 상태가 되었거나 상태를 저장한 이후인지를 확인하는것
(OS 버전 마다 다른데, onStop() 이후에 onSaveInstanceState() 호출 됨)
```java
if (fragmentManager.isStateSaved()) {  
	transaction.commitAllowingStateLoss();  
} else {  
	transaction.commit();  
}
```

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


### commit() / commitNow()
트랜잭션의 commit을 예약, commit은 즉시 수행되지 않음
commit은 다음 번 스레드가 준비될 때 메인 스레드에 대한 작업으로 예약
내부적으로 handler.post() 사용
기존에 만약 바로 수행하고 싶었다면, excutePendingTransactions() 을 사용했으나 의도하지 않게 다른 pending transaction 들을 수행하므로 주의해야했음

commitNow 는 동기식으로 바로 수행 됨
commit(), commitNow() 를 같이 사용하는 경우 순서를 보장 할 수 없음
그래서 발생할 문제를 차단하는 명목으로 commitNow() 에는 BackStack 을 사용할 수 없도록 함 (순서 보장이 안되니 back stack 도 보장 못하므로) 

> FragmentManager.findFragmentById() 를 해보면 동기/비동기의 차이를 왜 두었는지 이해 됨

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1OTM3NTUzOTEsNTMxMTg4OTQ3LC0xND
UzNjc5OTMwLDExNzk4Mzk5MTUsMTMxMjQwMDQyNCwtMjAyMDUw
OTk0OCwxMzQyNzk0ODY2LC0xOTc4MDI5MDI2LC0xMjAxNjE4OT
BdfQ==
-->