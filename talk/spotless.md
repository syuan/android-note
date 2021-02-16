

## Spotless

https://github.com/diffplug/spotless/tree/main/plugin-gradle

Spotless is a general-purpose formatting plugin used by 4,000 projects on GitHub (August 2020).

#### build.gradle
```groovy
plugins {  
  id "com.diffplug.spotless" version "5.2.0"  
}  
  
spotless {  
  kotlin {  
  target "**/*.kt"  
  ktlint('0.38.1').userData(['max_line_length' : '160'])  
   }  
}
```


#### java
```groovy
spotless {
  java {
    googleJavaFormat()
    // optional: you can specify a specific version and/or switch to AOSP style
    googleJavaFormat('1.7').aosp()
  }
}
```



<!--stackedit_data:
eyJoaXN0b3J5IjpbODg5Nzg5NDQxLC03MzExOTM3MjMsLTE5Mj
MxNDI5MF19
-->