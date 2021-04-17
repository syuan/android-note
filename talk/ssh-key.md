

# SSH Key

> https://opentutorials.org/module/432/3742
> https://arsviator.blogspot.com/2015/04/ssh-ssh-key.html


서버에 접속 할 때 비밀번호 대신 key를 제출하는 방식

#### SSH key 생성
키를 생성하면 공개키와 비공개키
SSH Key를 통해서 서버에 접속 할 때 Unix 계열(리눅스, 맥)에서는 ssh-keygen 사용


| file          | description                                   | 
|---------------|-----------------------------------------------|
|id_rsa         |private key                                    | 
|id_rsa.pub     |public key, remote의 authorized_keys 파일에 추가  |
|authorized_keys|remote의.ssh 디렉토리에 위치 id_rsa.pub 키의 값을 저장 |


이 중에 비공개키는 client 에 위치해야 하고, 공개키는 server (remote)에 위치
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQzODg4Mjc2OCwtMTExOTcyNTgxNiwxMj
kyNDczODU0XX0=
-->