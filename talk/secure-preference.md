
# How to Secure Android Shared Preferences?

이미 많은 개발자들은 SharedPreference 의 데이터를 암호화 하기 위해 라이브러리를 사용하고 있음 
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
eyJoaXN0b3J5IjpbLTQ2MjE1NzE1MF19
-->