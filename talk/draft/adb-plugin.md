


## ADB plugin



``` shell
adb shell dumpsys activity [package name]
```
현재 프로젝트의 activity / fragment stack 을 확인하는 android studio plugin 만들기

```
<depends>com.intellij.modules.platform</depends>
<depends>org.jetbrains.android</depends>
```
의존성을 잘 추가하면 기존보다 기본 동작을 쉽게 구현할 듯
- draft 형태로 일단 동작만 가능하게 만들것

- 메뉴 추가 위치 다시 체크
- 연결된 device 복수개 처리
- package 이름은 현재 프로젝트의 application id 로 처리할까?
- 명령어 수행을 비동기로 처리해야되나? / dialog 하나 띄우고 비동기로 간단하게 처리할까 (progress bar)
- 다이얼로그 사이즈를 유연하게 만드는건 고민, 기본 다이얼로그 깔끔하게 못만드나


https://github.com/NiTnEuQs/platform_tools_adt_idea/blob/c8a54a8ffd114264861a6080ea5dfe843c6b6968/android/src/org/jetbrains/android/run/AndroidRunningState.java


https://plugins.jetbrains.com/plugin/7380-adb-idea

https://github.com/pbreault/adb-idea/blob/master/src/main/resources/META-INF/plugin.xml

https://github.com/pbreault/adb-idea/blob/master/src/main/kotlin/com/developerphil/adbidea/adb/AdbFacade.kt
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NTkwMTgyMDksMTU3NDg3NzAxOCwtMz
g5NjgzOTM0XX0=
-->