

> https://github.com/aerogear/aerogear-android-sdk/blob/a18fe89d9b82e8fbaa518f5e3dffc2f0243b6d4f/build.gradle


```groovy
task jacocoRootReport(type: JacocoReport) {  
  apply plugin: 'jacoco'  
  
  jacoco {  
  toolVersion "0.8.7"  
  }  
  
  group = 'Reporting'  
  description = 'Generate Jacoco root coverage reports'  
  
  subprojects {  
  afterEvaluate { project ->  
  project.tasks.each { task ->  
  if (task.name.contains("jacocoTestReport")) {  
               dependsOn("${project.name}:jacocoTestReport")  
            }  
         }  
 } }  
  onlyIf = {  
  true  
  }  
  doFirst {  
  executionData.from = files(executionData.findAll {  
  it.exists()  
      })  
   }  
  
  def fileFilter = [  
         '**/R.class',  
         '**/R$*.class',  
         '**/*$ViewInjector*.*',  
         '**/BuildConfig.*',  
         '**/test/**/*.*',  
         '**/Manifest*.*',  
         'android/**/*.*'  
  ]  
  
    def modules = subprojects.findAll {!(it.name.contains("lightspeed") || it.name.contains("global"))}  
  
  def sourceDirs = []  
   modules.each { project -> sourceDirs << "$project.projectDir/src/main/java" }  
  sourceDirectories.from = files(sourceDirs)  
   additionalSourceDirs.from = files(sourceDirs)  
  
   def classDirs = []  
   modules.each { project -> classDirs << fileTree(dir: "$project.buildDir/intermediates/javac/debug", excludes: fileFilter) }  
  modules.each { project -> classDirs << fileTree(dir: "$project.buildDir/tmp/kotlin-classes/debug", excludes: fileFilter) }  
  classDirectories.from = files(classDirs)  
  
   def execData = []  
   modules.each { project -> execData << fileTree(dir: project.projectDir, includes: ['*.exec']) }  
  modules.each { project -> execData << fileTree(dir: project.buildDir, includes: ['outputs/code-coverage/connected/*coverage.ec']) }  
  executionData.from = files(execData)  
  
   reports {  
  xml.enabled = true  
  html.enabled = true  
  csv.enabled = false  
  }  
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMjMxNTM3NCwxMjEyMDc3MjQ0LDE3NT
MxMTk3MTJdfQ==
-->