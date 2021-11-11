


## Use LiveData to control button states

> https://developer.android.com/codelabs/kotlin-android-training-quality-and-states#0

Q. MVP 로 구현한다고 생각해보자
- stop 버튼을 누르면 night key 를 다음 fragment 로 옮기고 
- 그 fragment 에서 quality 를 선택한 다음 db 에 저장하고 이전 fragment 로 돌아옴

Q. click listener 를 어떻게 연결하고, 어떤 layer 에서 fragment 이동을 할것인가?



LiveData 에 nonnull 로 선언하고 null 을 설정하는게 허용이 되나??

navigation component 의 클래스들이 자동으로 생성이 잘 안되네, 
build 가 되긴하는데
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI2MDEyMDcxMCwxNTg2OTc2ODY1XX0=
-->