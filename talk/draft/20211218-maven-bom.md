


## Maven BOM (bill of materials)

> https://docs.gradle.org/current/userguide/platforms.html
> https://docs.gradle.org/current/userguide/platforms.html#sub:bom_import
> https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html#Importing_Dependencies


```groovy
dependencies {
    // import a BOM
    implementation platform('org.springframework.boot:spring-boot-dependencies:1.5.8.RELEASE')

    // define dependencies without versions
    implementation 'com.google.code.gson:gson'
    implementation 'dom4j:dom4j'
}
```

BOM 
- 프로젝트 의존성 버전 제어를 위한 POM
- 프로젝트 간에  dependency 를 공유하는 방법

platform() 은 의존성 버전을 제어할 수 있는 특수한 구성 요소


#### Firebase Bom
> https://firebase.google.com/docs/android/learn-more?hl=ko#bom
```groovy
dependencies {  
	implementation platform('com.google.firebase:firebase-bom:29.0.0')
	implementation 'com.google.firebase:firebase-config' 
	implementation 'com.google.firebase:firebase-analytics'
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTI2NTUwNjU1XX0=
-->