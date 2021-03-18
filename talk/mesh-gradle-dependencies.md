

# Gradle Dependencies: A Mesh


https://medium.com/swlh/gradle-dependencies-a-mesh-6e057a11326e


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

한 앱의 멀티 모듈은 동일한 dependency 버전을 사용해야 됨


<!--stackedit_data:
eyJoaXN0b3J5IjpbNDY2MTg0NzYyXX0=
-->