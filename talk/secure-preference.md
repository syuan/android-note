
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

Android Security 라이브러리는 크게 2가지 서비스와 Android KeyStore 활용한 MasterKeys generator을 제공한다.

-   암호화 관련 : EncryptedFile, EncryptedSharedPreferences
-   KeyAlias 생성 : Android KeyStore를 활용하여 MasterKeys generator 제공




<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg4NzA3NzAzMV19
-->