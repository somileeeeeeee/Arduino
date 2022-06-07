```dart
error Failed to install the app. Make sure you have the Android development environment set up: https://reactnative.dev/docs/environment-setup.
Error: Command failed: gradlew.bat app:installDebug -PreactNativeDevServerPort=8081

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:checkDebugAarMetadata'.
> A failure occurred while executing com.android.build.gradle.internal.tasks.CheckAarMetadataWorkAction
> The** minCompileSdk (31)** specified in a
dependency's AAR metadata (META-INF/com/android/build/gradle/aar-metadata.properties)
is greater than **this module's compileSdkVersion (android-30)**.
Dependency: androidx.core:core:1.7.0-alpha01.
AAR metadata file: C:\Users\gauraab\.gradle\caches\transforms-2\files-2.1\9e02d64f5889006a671d0a7165c73e72\core-1.7.0-alpha01\META-INF\com\android\build\gradle\aar-metadata.properties.
```
     
-> Error 이유 : MIN 컴파일 SDK : 31 이 나의 구성된 모듈 COMPILESDK버전이 낮아서 나는 오류

수정
![image](https://user-images.githubusercontent.com/30613069/172273943-ce71a7a1-b6d3-4ebb-ac3c-d109a117802c.png)

