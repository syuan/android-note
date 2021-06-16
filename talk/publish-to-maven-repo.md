

# Publish the library to a Remote Maven repository﻿

AGP 3.6.0 이상에서는 build artifact 를 Maven 저장소에 게시할 수 있는 Maven Publish Gradle 플러그인 지원 기능이 포함되어 있음
 
> https://developer.android.com/studio/build/maven-publish-plugin?hl=ko#groovy

```
    publishing {
        publications {
            // Creates a Maven publication called "release".
            release(MavenPublication) {
                // Applies the component for the release build variant.
                from components.release

                // You can then customize attributes of the publication as shown below.
                groupId = 'com.example.MyLibrary'
                artifactId = 'final'
                version = '1.0'
            }
            // Creates a Maven publication called “debug”.
            debug(MavenPublication) {
                // Applies the component for the debug build variant.
                from components.debug

                groupId = 'com.example.MyLibrary'
                artifactId = 'final-debug'
                version = '1.0'
            }
        }
    }
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ5MDIxMjYwMV19
-->