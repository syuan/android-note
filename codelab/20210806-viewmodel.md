

## ViewModel

> https://developer.android.com/codelabs/kotlin-android-training-view-model?hl=en&continue=https%3A%2F%2Fcodelabs.developers.google.com%2F%3Fcat%3Dandroid#4

ViewModel 생성 방법 - ViewModelProvider  
> https://readystory.tistory.com/176


AAC ViewModel 이 제공해주는 특징 중 하나는 activity, fragment lifecycle 보다 길게 상태를 관리해주는 것  
- rotation config 처럼 configuration change 가 발생했을때 onCreate 부타 다시 시작하면서 상태를 잃어버리게 되는데, ViewModel 의 lifecycle 이 더 길어서 onCreate 에서 다시 이전 data 를 사용할 수 있음 (ViewModelStore 에 ViewModel 이 저장되는듯?) 
- 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI4MjY5OTNdfQ==
-->