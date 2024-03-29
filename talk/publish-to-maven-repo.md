

# Publish the library to a Remote Maven repository﻿

AGP 3.6.0 이상에서는 build artifact 를 Maven 저장소에 게시할 수 있는 Maven Publish Gradle 플러그인 지원 기능이 포함되어 있음
  
> https://developer.android.com/studio/build/maven-publish-plugin?hl=ko#groovy
   
#### build.gradle (:sample-lib)
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

				pom {  
					name = 'My Library'  
					description = 'A concise description of my library'
					...
	            }
            
            // Creates a Maven publication called “debug”.
            debug(MavenPublication) {
                from components.debug
                
                groupId = 'com.example.MyLibrary'
                artifactId = 'final-snapshot'
                version = '1.0'

				pom {  
					name = 'My Library'  
					description = 'A concise description of my library'
					...
	            }
            }
        }
    }

	repositories {  
		maven {  
			name = 'Release'  
			url = "${rootProject.ext.publish.url}releases/"  
			credentials {  
				username = "${rootProject.ext.publish.user}"  
				password = "${rootProject.ext.publish.password}"  
			}  
		}
		  
		maven {  
			name = 'Snapshot'  
			url = "${rootProject.ext.publish.url}snapshot/"  
			credentials {  
				username = "${rootProject.ext.publish.user}"  
				password = "${rootProject.ext.publish.password}"  
			}  
		}
	}
}
```
from components.{variant} 를 선언하면 library module 의 경우,  
aar 이 artifact 로 등록됨  
  
직접 artifact 를 등록하기 싶은 경우  
```groovy
task sourceJar(type: Jar) {  
  from android.sourceSets.main.java.srcDirs  
   archiveClassifier.set('sources')  
}

artifact("$buildDir/outputs/aar/${project.name}-release.aar")  
artifact(sourceJar)
```

#### Gradle Task
```
publishAllPublicationsToReleaseRepository
publishAllPublicationsToSnapshotRepository

publishDebugPublicationToMavenLocal
publishDebugPublicationToReleaseRepository
publishDebugPublicationToSnapshotRepository

publishReleasePublicationToMavenLocal
publishReleasePublicationToReleaseRepository
publishReleasePublicationToSnapshotRepository
```

#### Publish to Maven Repository
```
./gradlew
clean
assebleRelase
publishReleasePublicationToReleaseRepository
```

#### pom.xml  (Project Object Model)
```
<project xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
    <modelVersion>4.0.0</modelVersion>  
    <groupId>com.example.MyLibrary</groupId>  
    <artifactId>final</artifactId>  
    <version>0.0.1</version>  
    <packaging>aar</packaging>  
    <name>My Library</name>  
    <description>A concise description of my library</description>  
      
    <dependencies>  
        <dependency>  
            <groupId>androidx.annotation</groupId>  
            <artifactId>annotation</artifactId>  
            <version>1.1.0</version>  
        </dependency>  
      
        <dependency>
            <groupId>com.squareup.okhttp3</groupId>  
            <artifactId>okhttp</artifactId>  
            <version>3.9.1</version>  
        </dependency>
    </dependencies>  
</project>
```

agp 4.2.2 로 업그레이드 이후 pom 파일 직접 만드는것과 aar 로 업로드가 안되서 
android, maven doc 에 나와있는 방식 대로 처리 
```
from components.release
```

pom.xml 의 의존성이 기존과 달라졌는데, 기존 dependency 는 compile 이 기본인데
pom.xml 이 자동으로 만들어지면 implementation 로 선언된 부분이 runtime 으로 선언되면서 기존이랑 차이가 생김
-> 그래서 implementation 선언된 부분을 api 로 바꿔주었음, 의미도 그것이 더 맞는것 같음

>https://maven.google.com/web/index.html#androidx.viewpager:viewpager:1.0.0
>https://docs.gradle.org/current/userguide/publishing_maven.html#publishing_maven:tasks
>https://developer.android.com/studio/build/maven-publish-plugin?hl=ko

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY3OTc3NTg4NiwxOTQ2NDUzMjU1LDEwNz
c3Njg3MzldfQ==
-->