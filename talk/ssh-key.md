

# SSH Key

> https://opentutorials.org/module/432/3742
> https://arsviator.blogspot.com/2015/04/ssh-ssh-key.html


서버에 접속 할 때 비밀번호 대신 key를 제출하는 방식

#### SSH key 생성
키를 만들면 공개키와 비공개키가 생성
이 중에 비공개키는 client 에 위치해야 하고, 공개키는 server (remote)에 위치

SSH Key를 통해서 서버에 접속 할 때 Unix 계열(리눅스, 맥)에서는 ssh-keygen 사용

| file          | description                                   | 
|---------------|-----------------------------------------------|
|id_rsa         |private key                                    | 
|id_rsa.pub     |public key, remote의 authorized_keys 파일에 추가  |
|authorized_keys|remote의.ssh 디렉토리에 위치 id_rsa.pub 키의 값을 저장 |

```
chmod 700 ~/.ssh

chmod 600 ~/.ssh/id_rsa

chmod 644 ~/.ssh/id_rsa.pub

chmod 644 ~/.ssh/authorized_keys

chmod 644 ~/.ssh/known_hosts
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc1NDY3MjY4OSwtMTExOTcyNTgxNiwxMj
kyNDczODU0XX0=
-->