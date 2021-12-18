

# Caused by android.content.res.Resources$NotFoundException: Unable to find resource ID #0x712345


```java
Caused by android.content.res.Resources$NotFoundException: Unable to find resource ID #0x712345
```



AppBundle 적용 이후 side load 의 문제
base APK와 configuration APKs, dynamic feature APKs 구성되는데, play store 이 외의 장소에서 다운로드 받아 base APK 만 설치하는 경우

```
density.enableSplit = false
```
분할 된 configuration apk 를 받지 않는 문제라서 density 분할을 disable 해서 해결할 수 있기는 함

```kotlin
class MyApplication : Application {  
    override fun onCreate() {  
        if (MissingSplitsManagerFactory.create(this).disableAppIfMissingRequiredSplits()) {  
            return  
        } super.onCreate()  
        ...  
    }  
}
```
또는 MissingSplitsManagerFactory 을 사용해서 마켓에서 다시 설치 하도록 유도할 수 도 있음

부정하게 설치한 사용자라서 대응할 필요는 없다고 생각됨, 사용하지 못하면 다시 제대로 설치할것이기 때문에
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjExMTkxOTE5NSwtMTI5MDA3NTE5NywxOD
UxODY4Nzc1LDczMDk5ODExNl19
-->