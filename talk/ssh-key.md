

# SSH Key

> https://opentutorials.org/module/432/3742
> https://arsviator.blogspot.com/2015/04/ssh-ssh-key.html


서버에 접속 할 때 비밀번호 대신 key를 제출하는 방식

#### SSH key 생성
키를 생성하면 공개키와 비공개키가 만들어진다. 
SSH Key를 통해서 서버에 접속 할 때 Unix 계열(리눅스, 맥)에서는 ssh-keygen 사용


id_rsa | private key, 절대로 타인에게 노출되면 안된다. 
-------------
|
id_rsa.pub

public key, 접속하려는 리모트 머신의 authorized_keys에 입력한다.

authorized_keys

리모트 머신의 .ssh 디렉토리 아래에 위치하면서 id_rsa.pub 키의 값을 저장한다. 자세한 내용은 다음 단락을 참조

이 중에 비공개키는 client 에 위치해야 하고, 공개키는 server(remote)에 위치해야 한다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUwNzkyMzgwNSwtMTExOTcyNTgxNiwxMj
kyNDczODU0XX0=
-->