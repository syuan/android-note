
# How to Secure Android Shared Preferences?

이미 많은 개발자들은 이것과 무관하게 암호화 라이브러리를 매우 잘 활용
https://github.com/scottyab/secure-preferences deprecated
https://github.com/facebookarchive/conceal

## Work with data more securely
https://developer.android.com/topic/security/data#java

AndroidX에 Android Security 라이브러리를 추가됨
```
dependencies { 
	implementation "androidx.security:security-crypto:1.0.0-rc03"
}
```



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5Mjk2MjQ2OTFdfQ==
-->