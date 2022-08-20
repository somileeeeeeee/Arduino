# 비밀번호 잃어버린 화면 만들기

1. 전체 화면.dart
![image](https://user-images.githubusercontent.com/30613069/185732911-2c1471bb-2d0c-4d26-9077-4a83ef0e6a40.png)

```dart
import 'package:flutter/material.dart';
import 'package:hansol_wiki/screens/forgot_password/body.dart';

// 단축키 stl + tab
class ForgotPasswordScreen extends StatelessWidget {
  // routeName 정해주기!
  static String routeName = "/forgot_password";

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Forgot Password"),
      ),
      body: Body(),
    );
  }
}
```

> route정해줬으니, routes.dart에 경로 추가!
![image](https://user-images.githubusercontent.com/30613069/185732931-21367cbf-5717-4f76-8c48-6b92d5700788.png)

> 화면 추가했으니, sign_in 화면에서 import -> 후에 don'thave account는 따로 
```dart
import 'package:flutter/material.dart';
import 'package:hansol_wiki/components/no_account_text.dart';
import 'package:hansol_wiki/components/social_card.dart';
import 'package:hansol_wiki/constants.dart';
import 'package:hansol_wiki/screens/forgot_password/forgot_password_screen.dart';
import 'package:hansol_wiki/screens/sign_in/sign_form.dart';
import 'package:hansol_wiki/size_config.dart';

class Body extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return SafeArea(
      // widget으로 wrap 시키기
      child: SizedBox(
        // double.infinity -> 중앙정렬
        width: double.infinity,

        // Column-> Padding으로 감싸기
        child: Padding(
          padding:
              EdgeInsets.symmetric(horizontal: getProportionateScreenWidth(20)),

          // widget으로 감싸기
          child: SingleChildScrollView(
            // widget으로 한번 더 감싸기 -> SingleChildScrollView :
            // 안할 시엔 화면이 길어져서 스크롤해야 다 담기던 화면을 한 화면에 담기게함
            child: SingleChildScrollView(
              child: Column(
                children: [
                  SizedBox(height: SizeConfig.screenHeight * 0.04),
                  Text(
                    "어서오시라우 집사들 \n¯\_(ツ)_/¯",
                    textAlign: TextAlign.center,
                    style: TextStyle(
                      color: Color.fromARGB(255, 37, 9, 116),
                      fontSize: getProportionateScreenWidth(20),
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  Text(
                    "\n Sign in with your email and password \n or continue with social media",
                    // text 정렬은 style에선 뜨지 않음!
                    textAlign: TextAlign.center,
                  ),
                  SizedBox(height: SizeConfig.screenHeight * 0.08),
                  SignForm(),
                  SizedBox(height: SizeConfig.screenHeight * 0.08),
                  Row(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: [
                      // 위젯으로 감싸기
                      SocialCard(
                        icon: "assets/icons/google-icon.svg",
                        press: () {},
                      ),

                      SocialCard(
                        icon: "assets/icons/facebook-2.svg",
                        press: () {},
                      ),

                      SocialCard(
                        icon: "assets/icons/twitter.svg",
                        press: () {},
                      ),
                    ],
                  ),
                  SizedBox(height: getProportionateScreenHeight(20)),

                  // Row -> Widget으로 추출
                  NoAccountText(),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

> NoAccount 는 components 폴더에 따로 빼줘서 클릭 시, ForgotPassword 스크린 넘어가도록 설정
![image](https://user-images.githubusercontent.com/30613069/185733050-265b0b1b-cebf-42df-a892-cce2fd77fc73.png)

2. Forgot_password body.dart 화면
![image](https://user-images.githubusercontent.com/30613069/185733091-50b1f710-d616-4e9a-a88a-984642e29226.png)

-> column으로 감쌀 시, 화면이 치우쳐짐
![image](https://user-images.githubusercontent.com/30613069/185733146-f46b75bd-f3ae-4096-a95b-40db08c0632d.png)





