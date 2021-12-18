

# Caused by android.content.res.Resources$NotFoundException: Unable to find resource ID #0x712345


```java
Caused by android.content.res.Resources$NotFoundException: Unable to find resource ID #0x712345
```



AppBundle 적용 이후 side load 의 문제
base APK와 configuration APKs, dynamic feature APKs 구성되는데, play store 이 외의 장소에서 다운로드 받아 base APK 만 설치하는 경우

```
density.enableSplit = false
```
분할 된 configuration apk 를 받지 않는 문제라서 density 분하ㅏㄹ으
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYyNzY5MDcwNywtMTI5MDA3NTE5NywxOD
UxODY4Nzc1LDczMDk5ODExNl19
-->