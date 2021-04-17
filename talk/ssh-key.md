

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
  
client 에서 생성한 id_res.pub 을 remote 의 authorized_keys 에 추가해야함
authorized_keys 의 복수개의 공개키를 가질수 있으니 append 할 것 
  
> ssh-copy-id 라는 유틸리티를 사용하면, remote server 에 id_pub 를 authorized_keys 에 추가해줌
  
``` 
chmod 700 ~/.ssh

chmod 600 ~/.ssh/id_rsa

chmod 644 ~/.ssh/id_rsa.pub

chmod 644 ~/.ssh/authorized_keys

chmod 644 ~/.ssh/known_hosts
```
파일 권한은 위와 같이 설정하는게 좋음


#### SSH 사용 방법

``` sh
$ ssh <ip>
```

``` sh
$ ssh <id_rsa path> <ip>
```

#### SSH 동작 원리
remote server에 SSH 데몬이 설치되어 있어야 가능
SSH 설치시 비대칭키 생성

##### 서버 인증 과정
1. client 가 server에 SSH 시도하면, 서버의 공개키를 받아와 .ssh/known_hosts 저장
2. client 받은 공개키로 난수를 암호화해서 server 전달 (난수의 hash 값을 저장해둠)
3. server 는 비밀키로 client 로 부터 받은 암호화된 난수를 복호화
4. server 는 알아낸 난수의 hash 값을 client 로 전달
5. client 는 처음 만든 난수의 hash 와 server 로 붙은 hash 를 비교

##### 사용자 인증 과정
1. server 는 난수를 하나 만들어서 암호화해서 client 로 전달 (authorized_keys 에 저장된 공개키로 암호화) (난수는 저장해둠)
2. client 는 server 로 부터 받은 암호화된 난수를 비밀키로 복호화
3. client 는 복호화된 난수의 hash 값을 서버로 전달
4. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA2MTk0NDY0NCwtMTkxMjk3NzY0MCwxOD
I0NDc3NDIsLTExMTk3MjU4MTYsMTI5MjQ3Mzg1NF19
-->