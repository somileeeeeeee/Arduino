# 로그인 성공 화면
## 완성 화면
![image](https://user-images.githubusercontent.com/30613069/185786689-b8ad1bc1-00f0-46be-aca4-6617fa9be7f4.png)


1. login_success_screen.dart 생성
![image](https://user-images.githubusercontent.com/30613069/185784227-7a2b2048-2899-484a-b66a-3b7dd1fc7647.png)
```dart
import 'package:flutter/material.dart';

class LoginSuccessScreen extends StatelessWidget {
  static String routeName = "/login_success"; 

  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```

2. route.dart에 경로 추가
```dart
import 'package:flutter/widgets.dart';
import 'package:hansol_wiki/screens/forgot_password/forgot_password_screen.dart';
import 'package:hansol_wiki/screens/login_success/login_success_screen.dart';
import 'package:hansol_wiki/screens/sign_in/sign_in_screen.dart';
import 'package:hansol_wiki/screens/splash/splash_screen.dart';

// We use name route
// All our routes will be available here
final Map<String, WidgetBuilder> routes = {
  SplashScreen.routeName: (context) => SplashScreen(),
  SignInScreen.routeName: (context) => SignInScreen(),
  ForgotPasswordScreen.routeName: (context) => ForgotPasswordScreen(),
  LoginSuccessScreen.routeName: (context) => LoginSuccessScreen(),
  // "/sign_in": (context) => SignInScreen()
};
```

3. sign_form.dart에 모든 인증이 완료되면 성공화면으로 넘어갈 수 있도록 추가
![image](https://user-images.githubusercontent.com/30613069/185784372-5ac189ac-84ee-429c-9b1d-b2d0e5bedd2d.png)

3-1. 현재는 Continue 누르면 그냥 넘어가버림 -> validator 뒤에 return "" 추가
![image](https://user-images.githubusercontent.com/30613069/185784560-ee998c25-4c5e-43ce-8c9d-247b18cea98f.png)

4. Body.dart 추가
```dart
import 'package:flutter/material.dart';
import 'package:hansol_wiki/components/default_button.dart';
import 'package:hansol_wiki/size_config.dart';

class Body extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return SizedBox(
      width: double.infinity,
      child: Column(
        // 밑으로 화면 추가
        children: [
          // 테스형 하트 사진
          SizedBox(height: SizeConfig.screenHeight * 0.04),
          Image.asset(
            "assets/images/love.jpg",
            height: SizeConfig.screenHeight * 0.4, //40%
          ),
          // 로그인성공 텍스트
          Text(
            "LOGIN SUCCESS",
            style: TextStyle(
              fontSize: getProportionateScreenWidth(25),
              fontWeight: FontWeight.normal,
              color: Colors.black,
            ),
          ),
          Spacer(),

          SizedBox(
            width: SizeConfig.screenWidth * 0.6,
            child: DefaultButton(
              text: "BACK TO HOME",
              press: () {},
            ),
          ),
          Spacer(),
        ],
      ),
    );
  }
}
```
