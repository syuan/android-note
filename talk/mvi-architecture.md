

# MVI Architecture with Android

### Background

사용자와의 인터렉션 또한 기존 서비스보다 훨씬 많아졌다. 그로 인해서 많은 버그가 발생하게 되었고 수 많은 양방향의 데이터 흐름 때문에 버그를 수정하기도 힘들었다

### Unidirectional data flow architecture 

Unidirectional data flow architecture 
Flux, Redux, MVI

Flux: Facebook이 만든 단방향 구조
View — Action — Dispacther — Store
Dispatcher는 EventBus, Otto, RxBus 등으로 구현할 수 있는 전역 이벤트 전달자

Redux: Redux는 Flux에서 고안한 State 관리 라이브러리
View — Action — Middleware — Reducer — Store

데이터가 **집중화(Centralized)** 되어 있어서 **예측 가능하며(Predictable)**데이터 흐름이 단방향이라서 **디버깅하기 쉽다(Debuggable)**. 또 리덕스와 연관된 좋은 생태계가 구축되어 있어서 필요에 맞게 **유연하게(Flexible)** 구현할 수 있다.


### MVI

Hannes Dorfmann
http://hannesdorfmann.com/android/mosby3-mvi-1
https://github.com/sockeqwe

<!--stackedit_data:
eyJoaXN0b3J5IjpbMzQyMTE2NjgsLTIwOTAxNjY5OTUsLTQ0NT
k4MTI2MCw4ODE0MTk2MTEsLTE5MDczMzI5NF19
-->