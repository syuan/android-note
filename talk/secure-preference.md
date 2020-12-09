
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
> 해당 라이브러리는 minS


Android Security 라이브러리는 크게 2가지 서비스와 Android KeyStore 활용한 MasterKeys generator을 제공한다.

-   암호화 관련 : EncryptedFile, EncryptedSharedPreferences
-   KeyAlias 생성 : Android KeyStore를 활용하여 MasterKeys generator 제공


EncryptedSharedPreferences은 기존 SharedPreferences에 약간의 코드 수정만으로도 암호화를 적용 가능

```
KeyGenParameterSpec spec = new KeyGenParameterSpec.Builder(  
      "_androidx_security_master_key_",  
      KeyProperties.PURPOSE_ENCRYPT | KeyProperties.PURPOSE_DECRYPT)  
      .setBlockModes(KeyProperties.BLOCK_MODE_GCM)  
      .setEncryptionPaddings(KeyProperties.ENCRYPTION_PADDING_NONE)  
      .setKeySize(256)  
      .build();  
  
MasterKey MasterKey = new MasterKey.Builder(this)  
      .setKeyGenParameterSpec(spec)  
      .build();  
  
SharedPreferences sharedPreferences = EncryptedSharedPreferences.create(  
      this,  
      "secret_shared_prefs",  
      MasterKey,  
      EncryptedSharedPreferences.PrefKeyEncryptionScheme.AES256_SIV,  
      EncryptedSharedPreferences.PrefValueEncryptionScheme.AES256_GCM);
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQxNjk2Mjk1NCwtMTYwNzgwOTE2NF19
-->