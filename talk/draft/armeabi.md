


### abi

"arm64-v8a", "armeabi-v7a", "armeabi"

ABI 라 함은 Application binary interface 로써 프로세서와 OS간을 주로 연결해주는 아주 낮은 레벨의 인터페이스
ARM 기반 cpu들과 x86기반 cpu들은 opcode구성이 다르기에 abi로 중재하여 os를 구현

안드로이드가 x86기반 cpu를 지원하게 된것이 최근입니다. 그래서 예전 api레벨에선 x86 관련 abi가 보이지 않지요

armeabi-v7a과 armeabi 는 단지 버전차이라고 보시면 됩니다.

v7a가 멀티미디어 관련 기능이 더 추가되었다고 합니다.

커널단에 가까운곳을 빌드하시는게 목적이시면 따로 질문주거나 메일주셔요 아는한 도와드리겠습니다.

정정합니다. v7a에서 멀티미디어 관련 기능이 강화된것이 아니고

neon 관련 명령어셋이 추가됨으로써 연산량이 증가해 멀티미디어 성능이 향상된것이라고 합니다.

멀티미디어 성능이 좋아진건 그냥 부가적인 현상
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzkzMzIyOTgzXX0=
-->