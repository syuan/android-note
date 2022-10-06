


> https://velog.io/@wodyd202/Hystrix-%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80


threshold 5? 이상 발생하면 1분 차단
threshold 10? 10분 차단

backoff


-   대기 시간은 min((2^n,  `random_number_milliseconds`),  `maximum_backoff`)입니다. 여기서  `n`은 반복(요청)마다 1씩 증가합니다.
    
-   `random_number_milliseconds`는 1,000밀리초 이하의 임의 숫자입니다. 이는 많은 클라이언트가 동기화되고 모든 요청이 한 번에 재시도되어 동기화된 웨이브로 요청을 보내는 경우를 피하는 데 도움이 됩니다.  `random_number_milliseconds`  값은 각 재시도 요청 후 다시 계산됩니다.
    
-   `maximum_backoff`는 일반적으로 32 또는 64초입니다. 적절한 값은 사용 사례에 따라 다릅니다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMDc2ODk0MTIsLTQ1NzEyMDQ3XX0=
-->