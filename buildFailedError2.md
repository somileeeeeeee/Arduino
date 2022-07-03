# 또 빌드에러..!?

![image](https://user-images.githubusercontent.com/30613069/177028873-b68669ad-216d-488f-a6f5-f5c3027ccddd.png)

> 1차로 해결했다고 생각했으나 여전히 해결되지 않음....

```shell
PS C:\Users\user\Hansol_wiki> flutter --version
Flutter 2.10.5 • channel stable • https://github.com/flutter/flutter.git
Framework • revision 5464c5bac7 (3 months ago) • 2022-04-18 09:55:37 -0700
Engine • revision 57d3bac3dd
Tools • Dart 2.16.2 • DevTools 2.9.2
PS C:\Users\user\Hansol_wiki> flutter doctor
Doctor summary (to see all details, run flutter doctor -v):
[√] Flutter (Channel stable, 2.10.5, on Microsoft Windows [Version 10.0.19044.1766], locale ko-KR)
[!] Android toolchain - develop for Android devices (Android SDK version 32.1.0-rc1)
    X cmdline-tools component is missing
      Run `path/to/sdkmanager --install "cmdline-tools;latest"`
      See https://developer.android.com/studio/command-line for more details.
    X Android license status unknown.
      Run `flutter doctor --android-licenses` to accept the SDK licenses.
      See https://flutter.dev/docs/get-started/install/windows#android-setup for more details.
[√] Chrome - develop for the web
[X] Visual Studio - develop for Windows
    X Visual Studio not installed; this is necessary for Windows development.
      Download at https://visualstudio.microsoft.com/downloads/.
      Please install the "Desktop development with C++" workload, including all of its default components
[!] Android Studio (not installed)
[√] Connected device (4 available)
[√] HTTP Host Availability

! Doctor found issues in 3 categories.
```
1. 안드로이드  Toolchain 이슈의 경우 

 - 나의 경우는 ToolChain 설치가 안되어서 일어났고, 일반적으로 안드로이드의 SDK 사용동의가 제대로 되지 않는 경우 입니다. 

> flutter doctor --android-licenses 를 터미널에서 실행 해 줍니다.

일반적인 경우 위 커맨드로 해결이 됩니다만 java.lang.NoClassDefFoundError  오류가 나타날때가 있습니다. 이 오류는 Android SDK Command Line Tool  이 설치 되지 않은 경우 입니다.

![image](https://user-images.githubusercontent.com/30613069/177029569-4753c94f-24a0-40ab-be72-72ac95e13418.png)

> 1. 안드로이드 스튜디오를 실행 하고 Preference -> SystemSetting ->  Androiㄴd SDK -> 오른쪽 화면에  SDK Tools -> 하단 Android SDK Command-line Tools 선택  후 다음 진행
> 2. 이 이후에 터미널로 돌아가셔서  **flutter doctor --android-licenses **  를 실행 합니다. 라이센스 사용에 대한 동의를 뭍는 질문이 3개 정도 나오는데 y 를 선택 후 진행 하시면 됩니다.

![image](https://user-images.githubusercontent.com/30613069/177029811-3382ad85-b76e-482e-a59b-bd1a9e228a92.png)
-> 안드로이드 관련 이슈는 정리되었고.. VS 는 C++ 를 사용한 데스크톱 개발 부분을 설치해줘야해서 다운
https://visualstudio.microsoft.com/ko/downloads/

![image](https://user-images.githubusercontent.com/30613069/177029938-5ac28340-6e6f-4736-ab1e-1cb91a6fbf6e.png)

## 또 다른 빌드ㅇㅔ러,,,,
: 엄청난 많은 에러가 났는데,,,, demon 어쩌고 저쩌고
``` cmd
FAILURE: Build failed with an exception.


* What went wrong:

Unable to start the daemon process.

This problem might be caused by incorrect configuration of the daemon.

For example, an unrecognized jvm option is used.

Please refer to the User Manual chapter on the daemon at https://docs.gradle.org/5.6.2/userguide/gradle_daemon.html

Process command line: C:\Program Files (x86)\Java\jre1.8.0_221\bin\java.exe -Xmx1536M -Dfile.encoding=windows-1252 -Duser.country=US -Duser.language=en -Duser.variant -cp C:\Users\ajoris\.gradle\wrapper\dists\gradle-5.6.2-all\9st6wgf78h16so49nn74lgtbb\gradle-5.6.2\lib\gradle-launcher-5.6.2.jar org.gradle.launcher.daemon.bootstrap.GradleDaemon 5.6.2

Please read the following process output to find out more:
```
![image](https://user-images.githubusercontent.com/30613069/177030514-3e979e38-40d4-4633-aeba-f3fa60b4372e.png)
From:

org.gradle.jvmargs=-Xmx1536M

To:

org.gradle.jvmargs=-Xmx1024M
-> ㅣㅇ렇게 용량을 바꿔주었떠니...
드디어 빌드 성공!!!!!!!!!!!!!!!!!!!!!!!! ❣
