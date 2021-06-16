

# Publish the library to a Remote Maven repository﻿

AGP 3.6.0 이상에서는 build artifact 를 Maven 저장소에 게시할 수 있는 Maven Publish Gradle 플러그인 지원 기능이 포함되어 있음
  
> https://developer.android.com/studio/build/maven-publish-plugin?hl=ko#groovy
   
build.gradle (:sample-lib)
```groovy 
apply plugin: 'maven-publish'

...

afterEvaluate {
    publishing {
        publications {
            // Creates a Maven publication called "release".
            release(MavenPublication) {
                from components.release
                
                groupId = 'com.example.MyLibrary'
                artifactId = 'final'
                version = '1.0'
            }
            
            // Creates a Maven publication called “debug”.
            debug(MavenPublication) {
                from components.debug
                
                groupId = 'com.example.MyLibrary'
                artifactId = 'final-snapshot'
                version = '1.0'
            }
        }
    }
}
```


```groovy
task sourceJar(type: Jar) {  
  from android.sourceSets.main.java.srcDirs  
   archiveClassifier.set('sources')  
}

artifact("$buildDir/outputs/aar/${project.name}-release.aar")  
artifact(sourceJar)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU2NTU5NjU1NCwtMjA2ODI4MzQxNl19
-->