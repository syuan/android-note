


## abi

> https://developer.android.com/ndk/guides/abis?hl=ko
"arm64-v8a", "armeabi-v7a", "armeabi", "x86", "x86_64"

abi 라 함은 application binary interface 로 프로세서와 OS간을 주로 연결해주는 interface
arm cpu 와 x86 cpu 들은 opcode구성이 다르기에 abi로 중재하여 os를 구현

런타임에 시스템과 앱의 머신코드가 어떻게 상호작용 할지를 기술한 인터페이스 
so파일을 로딩하는 경우, 머신코드-아키텍쳐에서 사용하는 ABI와 일치해야 구동이 가능

#### Arm cpu

"arm64-v8a", "armeabi-v7a", "armeabi"

armeabi 는 NDK r16에서 툴체인이 deprecated 

armeabi-v7a 과 armeabi 는 단지 버전차이
v7a 는 neon 관련 명령어셋이 추가되어 연산량 증가 (멀티미디어 성능이 향상)

arm64-v8a 은 64-bit 지원

arm64-v8a기기를 예로 들면,  armeabi와 armeabi-v7a 코드도 실행할 수 있다. 다만 앱이 arm64-v8a를 대상으로 하는 경우 32비트의 기기보다 64비트 기기에서 더욱 잘 수행

#### Intel cpu

"x86", "x86_64"
32bit, 64bit 차이

많은 X86 기반 기기는 armeabi-v7a 및 armeabi NDK 바이너리도 실행할 수 있다. 이런 기기의 경우 Primary ABI가 X86, Secondary ABI는 armeabi-v7a


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NzY3MzM4ODUsLTYzMjYzNjczNV19
-->