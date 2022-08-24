



기본적으로 singleton 이고 provider 를 통해서 context 주입 받음

thread pool 의 thread 기본값은 3, 네트워크 상태에 따라 변경됨
PriorityBlockingQueue


초기화 시점에 context 를 통해서 network 상태 변화 감지를 위한 NetworkBroadcastReceiver 를 등록

android.util.LruCache

Bitmap.prepareToDraw() ?


Handler.hasMessages() : sendEmptyMessageDelayed 로 보낸 message 가 있는지 체크하는 군

dispatcher 는 전체적인 요청들을 처리, 중간 연결자 역할?, handler 를 갖고 모든 요청(Action) 을 순차적으로 처리


1. 옵션 정보와 함께 Request 를 만들고, 
2. memcache 확인, 이전 요청 취소
3. Action 이라는 객체를 생성, request, target, callback 의묶음
4. 같은 target 이 있으면 기존 요청 취소, 
5. Action 을 dispatcher 에 submit()
6. Hunter (Runnable) 을 만듬, action, cache, dispatcher 를 갖고 실제 http request 역할
7. Hunter 를 ExecutorService 에 submit()
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQwMjYyNzYyMCwxMDkzMTk4MDM0LDExNz
g3NjAwMzcsLTEyMDMwMjQ1OTVdfQ==
-->