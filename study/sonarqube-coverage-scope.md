



요구하는 test coverage package 는 model, presenter, interactor 로 제한하는 방법

1. jacoco gradle plugin 을 통해서 생성하는 test coverage report (xml, html) 에 package 를 제한하는 방법  
JacocoReport.classDirectories 값 (filetree 로 특정 package 지정)

2. sonarqube 에서 특정 package 를 제한하는 방법  
>https://docs.sonarqube.org/display/SONAR/Narrowing+the+Focus#NarrowingtheFocus-IgnoreFiles

아래 속성 사용
- sonar.inclusions  
- sonar.exclusions  


**sonarqube 에 적용하고 싶은 경우 2번 방법**
sonar.inclusions=**/model/**/*.*, **/interactor/**/*.*, **/presenter/**/*.*
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzE1OTI2NTM3XX0=
-->