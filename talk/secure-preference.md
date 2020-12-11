
# How to Secure Android Shared Preferences?

이미 많은 개발자들은 SharedPreference 의 데이터를 암호화 하기 위해 라이브러리를 사용하고 있음. 

https://github.com/scottyab/secure-preferences deprecated  
https://github.com/facebookarchive/conceal  
  
## Work with data more securely
https://developer.android.com/topic/security/data#java
  
AndroidX에 Android Security 라이브러리를 추가됨. 
```
dependencies { 
	implementation "androidx.security:security-crypto:1.0.0-rc03"
}
```
> 해당 라이브러리는 minSdk 23 부터 사용 가능


Android Security 라이브러리는 크게 2가지 서비스와 Android KeyStore 활용한 MasterKeys generator을 제공한다.  

-   암호화 관련 : EncryptedFile, EncryptedSharedPreferences
-   KeyAlias 생성 : Android KeyStore를 활용하여 MasterKeys generator 제공


EncryptedSharedPreferences은 기존 SharedPreferences에 약간의 코드 수정만으로도 암호화를 적용 가능  
  
EncryptedSharedPreferences 생성 방법
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
 
SharedPreferences 사용하는 방법은 동일
```
SharedPreferences.Editor sharedPrefsEditor = sharedPreferences.edit();  
sharedPrefsEditor.apply();
```

저장된 데이터는 이렇게 암호화 되어있음
> /data/data/[packageName]/shared_prefs/[preferencesName].xml

```
<?xml version='1.0' encoding='utf-8' standalone='yes' ?>  
<map>  
    <string name="__androidx_security_crypto_encrypted_prefs_key_keyset__">12a70180ea09a6c7b404657423bcd19326b0b75d5f7087f8398c670eb82381b52ab13263289c5b7defb6fbd6b04088616bd2a74374c5d1c3bd959d1fee690c525a78b6dbcefd0e538b7d3491a506eac55fab99415a0cb0e9de7cbc41e79c9e6901d8016d06695d4eeb08bd98827d062f43cb1ca0a1fbcd87b4317655311c053dd955d3aa00cadd7c66b2e540be0022684b73c563bcbb3ca010141e40c4cb326f5aafe6f3b87c71561ade1a4208a9cbf854123b0a30747970652e676f6f676c65617069732e636f6d2f676f6f676c652e63727970746f2e74696e6b2e4165735369764b6579100118a9cbf8542001</string>  
    <string name="__androidx_security_crypto_encrypted_prefs_value_keyset__">1288011cc9d76e6eaf16d5b7f66640575684254c26cfe111f4a5d33bb320411974ac32600104cf6de82b196a4e19294f69a2fbbc05b991fac2584dc3dd102210261f885b521c80ed48bc3f64ae1f9088d92429e548ae3fe6bad8b601004a853e9df470bfc54a707614301cdc6fba35806ca61d951b2a080c1456871c189eb7b0e2c488cac918c42c0e231a1a440890d9cda301123c0a30747970652e676f6f676c65617069732e636f6d2f676f6f676c652e63727970746f2e74696e6b2e41657347636d4b657910011890d9cda3012001</string>  
    <string name="AQqeJakAK6T25Xzfk2H9Ux+qSOwaQx16L1WRrX4=">ARRzbJDa6Vn64x5pSgYyWP5ZjEgtEEvCtNWy1noBReNBBP1TvJybGq+dU8UPxTGvbAcb</string>  
</map>
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzk0OTk2NjY1LDE3Mzc5MDEwNzUsLTIzNT
k1NzM5LC0xNjA3ODA5MTY0XX0=
-->