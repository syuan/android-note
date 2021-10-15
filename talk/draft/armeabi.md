


## abi

> https://developer.android.com/ndk/guides/abis?hl=ko
"arm64-v8a", "armeabi-v7a", "armeabi", "x86", "x86_64"

abi 라 함은 application binary interface 로 프로세서와 OS간을 주로 연결해주는 interface
arm cpu 와 x86 cpu 들은 opcode구성이 다르기에 abi로 중재하여 os를 구현

#### Arm cpu

"arm64-v8a", "armeabi-v7a", "armeabi"

armeabi-v7a 과 armeabi 는 단지 버전차이
v7a 는 neon 관련 명령어셋이 추가되어 연산량 증가 (멀티미디어 성능이 향상)

arm64-v8a 은 64-bit 지원

#### Intel cpu (주로 )

"x86", "x86_64"
32bit, 64bit 차이


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMxNTk1ODY0NSwtNjMyNjM2NzM1XX0=
-->