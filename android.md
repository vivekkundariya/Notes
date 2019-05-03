
# Android

Import files for commonly used libraries listed below :-

## Android component
```
implementation 'androidx.recyclerview:recyclerview:1.0.0'
implementation 'androidx.cardview:cardview:1.0.0'
implementation 'androidx.appcompat:appcompat:1.0.2'
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
def room_version = "2.1.0-alpha07"

implementation "androidx.room:room-runtime:$room_version"
annotationProcessor "androidx.room:room-compiler:$room_version" // For Kotlin use kapt instead of annotationProcessor

// optional - Kotlin Extensions and Coroutines support for Room
implementation "androidx.room:room-ktx:$room_version"
```
