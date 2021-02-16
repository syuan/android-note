

## Spotless

https://github.com/diffplug/spotless/tree/main/plugin-gradle

Spotless is a general-purpose formatting plugin used by 4,000 projects on GitHub (August 2020).

```groov
spotless {
  java {
    googleJavaFormat()
    // optional: you can specify a specific version and/or switch to AOSP style
    googleJavaFormat('1.7').aosp()
  }
}
```



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkwODcxMzYzNSwtNzMxMTkzNzIzLC0xOT
IzMTQyOTBdfQ==
-->