

## Spotless

https://github.com/diffplug/spotless/tree/main/plugin-gradle

Spotless is a general-purpose formatting plugin used by 4,000 projects on GitHub (August 2020).

#### Usage
```
$ ./gradlew build
$ ./gradlew spotlessApply
```

#### build.gradle
```groovy
plugins {  
  id "com.diffplug.spotless" version "5.2.0"  
}  
  
spotless {  
  kotlin {  
  target "**/*.kt"  
  ktlint('0.38.1').userData(['max_line_length' : '100'])  
   }  
}
```


#### java
```groovy
spotless {
  java {
    removeUnusedImports()
    trimTrailingWhitespace()
    indentWithTabs()
    endWithNewline()
    
    googleJavaFormat()
    // optional: you can specify a specific version and/or switch to AOSP style
    googleJavaFormat('1.7').aosp()
  }
}
```

#### kotlin
```groovy
spotless { 
  kotlin {
    // by default the target is every '.kt' and '.kts` file in the java sourcesets
    ktfmt()    
    ktlint()   
    diktat()   
    prettier() 
  }
  kotlinGradle {
    target '*.gradle.kts' // default target for kotlinGradle
    ktlint() // or ktfmt() or prettier()
  }
}
```

> https://github.com/pinterest/ktlint

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg4MDg5MDcxNCwxMDgzODkzMDM4LDE3MD
U5NTMyMjMsLTczMTE5MzcyMywtMTkyMzE0MjkwXX0=
-->