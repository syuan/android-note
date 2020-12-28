

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


### MVI

Hannes Dorfmann
http://hannesdorfmann.com/android/mosby3-mvi-1
https://github.com/sockeqwe

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwOTAxNjY5OTUsLTQ0NTk4MTI2MCw4OD
E0MTk2MTEsLTE5MDczMzI5NF19
-->