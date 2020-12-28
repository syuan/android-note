

# MVI Architecture with Android



Unidirectional data flow architecture 
Flux, Redux, MVI

Flux: Facebook이 만든 단방향 구조
View — Action — Dispacther — Store
Dispatcher는 EventBus, Otto, RxBus 등으로 구현할 수 있는 전역 이벤트 전달자

Redux: Redux는 Flux에서 고안한 State 관리 라이브러리
View — Action — Middleware — Reducer — Store

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ0NTk4MTI2MCw4ODE0MTk2MTEsLTE5MD
czMzI5NF19
-->