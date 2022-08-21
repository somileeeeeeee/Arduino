# 비밀번호 잃어버린 화면 만들기
## 최종 화면
![image](https://user-images.githubusercontent.com/30613069/185781406-a722dda6-024d-4f29-9a7c-7bf0ac27eb9f.png)


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

> NoAccount Text는 components 폴더에 따로 빼줘서 다양한 화면에서 사용할 수 있도록 해줌
![image](https://user-images.githubusercontent.com/30613069/185781459-ac99f9e4-3a38-42a4-8f0b-b1cba13060b5.png)

```dart
import 'package:flutter/material.dart';
import 'package:hansol_wiki/constants.dart';
import 'package:hansol_wiki/size_config.dart';

class NoAccountText extends StatelessWidget {
  const NoAccountText({
    Key? key,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Text(
          "Don't have an account?",
          style: TextStyle(fontSize: getProportionateScreenWidth(16)),
        ),
        // Text -> Widget 감싸기
        GestureDetector(
          onTap: () {},
          child: Text(
            "Sign Up",
            style: TextStyle(
                fontSize: getProportionateScreenWidth(16),
                color: kPrimaryColor),
          ),
        ),
      ],
    );
  }
}
```

2. Forgot_password body.dart 화면
![image](https://user-images.githubusercontent.com/30613069/185733091-50b1f710-d616-4e9a-a88a-984642e29226.png)

-> column으로 감쌀 시, 화면이 치우쳐지는 현상이 있음. 이를 SizedBox로 감싸서 width: double.infinity로 정렬
![image](https://user-images.githubusercontent.com/30613069/185733146-f46b75bd-f3ae-4096-a95b-40db08c0632d.png)

-> Email Form 생성
![image](https://user-images.githubusercontent.com/30613069/185781559-b976a35d-41d0-406b-acd2-501119ec6d47.png)
> email 폼 복붙

-> 위에서 child: SingleChildScrollView로 Widget 변경해줘서 한화면에 보이게끔
```dart
import 'package:flutter/material.dart';
import 'package:hansol_wiki/components/custom_surfix_icon.dart';
import 'package:hansol_wiki/components/default_button.dart';
import 'package:hansol_wiki/components/form_error.dart';
import 'package:hansol_wiki/components/no_account_text.dart';
import 'package:hansol_wiki/constants.dart';
import 'package:hansol_wiki/size_config.dart';

class Body extends StatelessWidget {
  const Body({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // column으로 설정 시, 화면이 왼쪽으로 치우쳐저서
    // SizedBox로 감싸줌
    return SizedBox(
      width: double.infinity,
      child: SingleChildScrollView(
        child: Padding(
          padding:
              EdgeInsets.symmetric(horizontal: getProportionateScreenWidth(20)),
          child: Column(
            children: [
              SizedBox(height: SizeConfig.screenHeight * 0.04),
              Text(
                "Forgot Password",
                style: TextStyle(
                  fontSize: getProportionateScreenWidth(28),
                  color: Colors.black,
                  fontWeight: FontWeight.bold,
                ),
              ),
              Text(
                "Plz enter your email and we will send \nyou a link to return to your account",
                textAlign: TextAlign.center,
              ),
              SizedBox(height: SizeConfig.screenHeight * 0.1),
              ForgotPassForm(),
            ],
          ),
        ),
      ),
    );
  }
}

class ForgotPassForm extends StatefulWidget {
  @override
  _ForgotPassFormState createState() => _ForgotPassFormState();
}

class _ForgotPassFormState extends State<ForgotPassForm> {
  final _formKey = GlobalKey<FormState>();
  List<String> errors = [];
  String? email;

  @override
  Widget build(BuildContext context) {
    return Form(
      key: _formKey,
      child: Column(
        children: [
          // sign_form 복붙
          TextFormField(
            keyboardType: TextInputType.emailAddress,
            onSaved: (newValue) => email = newValue,
            onChanged: (value) {
              if (value.isNotEmpty && errors.contains(kEmailNullError)) {
                setState(() {
                  errors.remove(kEmailNullError);
                });
              } else if (emailValidatorRegExp.hasMatch(value) &&
                  errors.contains(kInvalidEmailError)) {
                setState(() {
                  errors.remove(kInvalidEmailError);
                });
              }
              return null;
            },
            validator: (value) {
              if (value!.isEmpty && !errors.contains(kEmailNullError)) {
                setState(() {
                  errors.add(kEmailNullError);
                });
              } else if (!emailValidatorRegExp.hasMatch(value) &&
                  !errors.contains(kInvalidEmailError)) {
                setState(() {
                  errors.add(kInvalidEmailError);
                });
              }
              return null;
            },
            decoration: InputDecoration(
              labelText: "Email",
              hintText: "Enter your email",

              // email 이란 건 위에 뜨고, 힌트텍스트는 테두리 안에 들어가도록
              floatingLabelBehavior: FloatingLabelBehavior.always,

              // 아이콘이 튀어나가서 Padding으로 감싸기
              // Padding을 Extract Widget시킴
              suffixIcon: CustomSurffixIcon(svgIcon: "assets/icons/Mail.svg"),
              contentPadding: EdgeInsets.symmetric(
                horizontal: 42,
                vertical: 20,
              ),
              enabledBorder: OutlineInputBorder(
                borderRadius: BorderRadius.circular(28),
                borderSide: BorderSide(color: kTextColor),
                gapPadding: 10,
              ),
              focusedBorder: OutlineInputBorder(
                borderRadius: BorderRadius.circular(28),
                borderSide: BorderSide(color: kTextColor),
                gapPadding: 10,
              ),
            ),
          ),
          SizedBox(height: getProportionateScreenHeight(30)),
          FormError(errors: errors),
          SizedBox(height: SizeConfig.screenHeight * 0.1),
          DefaultButton(
            text: "Continue",
            press: () {
              if (_formKey.currentState!.validate()) {
                // Do what you want to do
              }
            },
          ),
          SizedBox(height: SizeConfig.screenHeight * 0.1),
          NoAccountText(),
        ],
      ),
    );
  }
}
```

3. sign_form.dart에서 GestureDetector추가
![image](https://user-images.githubusercontent.com/30613069/185781646-6e773610-1774-439c-98c5-1c7ae1ddb5f8.png)
```dart
GestureDetector(
                onTap: () => Navigator.pushNamed(
                    context, ForgotPasswordScreen.routeName),
                child: Text(
                  "Forgot Password",
                  style: TextStyle(decoration: TextDecoration.underline),
                ),
              )
            ],
          ),
```          

