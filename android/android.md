
# Android

Import files for commonly used libraries listed below :-

# Project.gradle

```
buildscript {
  ext {
          kotlin_version = '1.3.30'
          roomVersion = '2.1.0-alpha06'
          archLifecycleVersion = '2.0.0'
      }
}
```

## Android component
```
implementation 'androidx.recyclerview:recyclerview:1.0.0' 
implementation 'androidx.cardview:cardview:1.0.0'
implementation 'androidx.appcompat:appcompat:1.0.2'
implementation 'androidx.core:core-ktx:1.0.1'
implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
implementation 'com.google.android.material:material:1.1.0-alpha05'
```

## Lifecycle components
```  
implementation "androidx.lifecycle:lifecycle-extensions:$rootProject.archLifecycleVersion"
kapt "androidx.lifecycle:lifecycle-compiler:$rootProject.archLifecycleVersion"
```

## Coroutine
```  
implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-core:1.1.1'
implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.1.1'
```

## Stetho
```
implementation 'com.facebook.stetho:stetho:1.5.1'
```

## Firebase
```
implementation 'com.google.firebase:firebase-core:16.0.8'
implementation 'com.google.firebase:firebase-config:16.5.0'
```

## Gson
```
implementation 'com.google.code.gson:gson:2.8.5'
```

## Room
```
implementation "androidx.room:room-runtime:$rootProject.roomVersion"
kapt "androidx.room:room-compiler:$rootProject.roomVersion"
androidTestImplementation "androidx.room:room-testing:$rootProject.roomVersion"
```

## OkHttp
```
implementation 'com.squareup.okio:okio:1.14.0'
implementation 'com.squareup.okhttp3:okhttp:3.10.0'
```

## Glide
```
implementation 'com.github.bumptech.glide:glide:4.9.0'
annotationProcessor 'com.github.bumptech.glide:compiler:4.9.0'
```
