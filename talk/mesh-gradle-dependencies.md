

# Gradle Dependencies: A Mesh


> https://medium.com/swlh/gradle-dependencies-a-mesh-6e057a11326e


라이브러리를 그룹 별로 구분  

```gradle
dependencies {  
  implementation "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"  
  
  implementation 'com.google.android.material:material:1.2.1'  
  
  implementation 'androidx.core:core-ktx:1.3.2'  
  implementation 'androidx.appcompat:appcompat:1.2.0'  
  implementation 'androidx.constraintlayout:constraintlayout:2.0.4'  
  implementation 'androidx.activity:activity-ktx:1.2.0-beta02'  
  implementation 'androidx.fragment:fragment-ktx:1.3.0-beta02'  
  
  implementation 'cn.bingoogolapple:bga-qrcode-zxing:1.3.7'  
  
  implementation 'com.squareup.retrofit2:retrofit:2.9.0'  
  implementation 'com.squareup.retrofit2:converter-gson:2.9.0'  
  implementation 'com.squareup.retrofit2:adapter-rxjava2:2.9.0'  
  implementation 'com.squareup.okhttp3:logging-interceptor:4.7.2'  
  
  implementation 'io.reactivex.rxjava2:rxandroid:2.1.1'  
  
  testImplementation 'junit:junit:4.13.1'  
  
  androidTestImplementation 'androidx.test.ext:junit:1.1.2'  
  androidTestImplementation 'androidx.test.espresso:espresso-core:3.3.0'  
}
```

한 앱의 멀티 모듈들은 동일한 dependency 버전을 사용할 필요가 있음  

app/build.gradle
```gradle
dependencies {  
  implementation kt  
    implementation meterial  
    implementation androidx  
    implementation qrcode  
    implementation retrofit  
    implementation rxjava  
  
    testImplementation junit  
    androidTestImplementation testing  
}
```

build.gradle
```
ext {  
  kt = [  
	  'org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version'  
  ]  
  
  meterial = [  
	  'com.google.android.material:material:1.2.1'  
  ]  
  
  androidx = [  
	  'androidx.core:core-ktx:1.3.2',  
      'androidx.appcompat:appcompat:1.2.0',  
      'androidx.constraintlayout:constraintlayout:2.0.4',  
      'androidx.activity:activity-ktx:1.2.0-beta02',  
      'androidx.fragment:fragment-ktx:1.3.0-beta02',  
  ]  
  
  qrcode = [  
	  'cn.bingoogolapple:bga-qrcode-zxing:1.3.7'  
  ]  
  
  retrofit = [  
	  'com.squareup.retrofit2:retrofit:2.9.0',  
      'com.squareup.retrofit2:converter-gson:2.9.0',  
      'com.squareup.retrofit2:adapter-rxjava2:2.9.0',  
      'com.squareup.okhttp3:logging-interceptor:4.7.2'  
  ]  
  
  rxjava = [  
	  'io.reactivex.rxjava2:rxandroid:2.1.1'  
  ]  
  
  junit = [  
	  'junit:junit:4.13.1'  
  ]  
  
  testing = [  
	  'androidx.test.ext:junit:1.1.2',  
      'androidx.test.espresso:espresso-core:3.3.0'  
  ]  
}
```

kotlin 이라는 이름은 안되네, 이미 정의된 이름인듯?
크게 가독성이 좋아지는 느낌은 아님, 멀티 모듈이라면 고민해볼 수 있을듯
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAyMzAwNDg5LDQ2NjE4NDc2Ml19
-->