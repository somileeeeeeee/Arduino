# 1. Flutter 이해하기
• Flutter는 모든 것이 위젯(Widget)으로 만들어져 있음. 위젯(Widget)은 레고 블록과 같이 앱을 만드는 데 사용되는 작은 모듈

• 위젯들을 조합해 화면을 그리는데, 이 위젯들의 조합이 나무와 같이 생겼다하여 위젯트리(Widget Tree)라고 부름.

• 어떤 위젯이 있는 지 알아보려면 ? -> https://docs.flutter.dev/development/ui/widgets

• 이 달의 위젯 -> Flutter Widget of the Week

• 다 기억 못하니까 메모할것..! -> https://velog.io/

• Flutter Community -> https://flutter.dev/community
![image](https://user-images.githubusercontent.com/30613069/172087473-eea1a850-574a-454c-8830-3e1f6beff7dd.png)


# 2. Android Material & Ios Cuptertino
• 메테리얼 위젯(Material Widget)은 Android에 기본 화면 구성 요소를 Flutter에서 그대로 재현한 위젯입니다.

• 쿠퍼티노 위젯(Cupertino Widget)은 iOS에 기본적으로 내장된 화면 구성 요소를 Flutter에서 재현한 위젯입니다.

• Flutter는 특정 플랫폼에 종속되지 않은 고유의 디자인을 입힌 커스텀 위젯(Custom Widget)도 쉽게 만들 수 있습니다.
![image](https://user-images.githubusercontent.com/30613069/172087497-2c7efccb-6485-442b-91d7-b122e7b56726.png)

•  https://docs.flutter.dev/development/ui/widgets

# 3. Dart 문법
• Flutter 코드를 작성하는 데 필요한 Dart 문법!

• DartPad : 온라인 상에서 Dart를 실행할 수 있는 웹사이트
https://dartpad.dev/?id=02d3c1600e40dd95d65af5ca6a3e4d16&null_safety=true

• 실행 순서 : java와 같이 main은 Dart 에서 처음 시작 시 호출하는 약속된 함수!

• // : 주석으로 컴퓨터가 읽지 않습니다. 주로 개발하면서 메모할 때 사용합니다.

• print() : print의 소괄호 안쪽에 값을 넣으면 오른쪽 Console에 값이 출력 됩니다. 정상적으로 잘 작동하는지 확인(디버깅) 할 때 사용합니다.

• ; : Dart에서는 마지막에 세미콜론(semicolon)을 찍어줍니다.

• 에러 로그 읽는 법
<br/>
  - 아래 이미지를 보면 3번 째 줄에 마지막 세미콜론이 빠졌습니다. 이 상태로 Run을 하게되면 우측에 에러 메세지가 나옵니다.
  <br/>
  - 에러 메세지를 보면 문제가 발생하는 위치와 해결 방법을 알 수 있습니다! 앞으로 에러가 발생한다면 에러 메세지 부터 확인해 주세요 🙂
<br/>

## 3-1. 변수
1. 변수 만들기
- 변수는 어떤 값을 잠시 보관하는 저장소!

![image](https://user-images.githubusercontent.com/30613069/172087639-48656b3f-60e2-42d7-9874-0b709a7a72ad.png)

- 자료형 (= 바구니에 담을 수 있는 값의 종류)

  `var` : 처음 담긴 값으로 타입이 지정됩니다.

  `String` : 문자만 담을 수 있습니다.

  `String?` : 문자 또는 비어있는(`null`) 상태일 수 있습니다.

  `final String` : 문자를 한 번 담은 뒤 재할당 불가능합니다.

- 변수명 (= 바구니 이름)
  💡 Dart의 변수명 만드는 규칙
  1. `영문` / `_` / `$` / `숫자`만 사용
  2. `숫자`로 시작 불가능
  3. 카멜케이스(camelCase) 사용

- 💡 카멜케이스(camelCase)란?
  - 소문자로 시작하며, 단어와 단어 사이를 대문자로 구분하는 방법
  - 낙타의 혹과 같이 생겨서 camelCase라고 부릅니다.
  - 예) helloWorld, whereAreYouFrom

- 예시
	```dart
main() {
  /// var : 처음 담은 값으로 자료형이 결정 됨
  var name = '철수';
  print(name); // 철수
  print(name.runtimeType); // string (문자)

  var age = 20;
  print(age); // 20
  print(age.runtimeType); // int (정수)


  print("="*20);


  /// String : 문자만 넣을 수 있음
  String address = '우리집';
  print(address); // 우리집

  // address = 1; // ⬅️ String 만 담을 수 있기 때문에 이 코드는 에러 발생

  address = '모두의 집';
  print(address); // 모두의 집


  print("="*20);


  /// String? : 문자 또는 비어있을 수 있음
  String? email; // ⬅️ 아무것도 안넣었으므로 비어있음
  print(email); // null ⬅️ 비어있음을 의미

  email = "a@a.com"; // 문자열 할당
  print(email); // a@a.com

  email = null; // 다시 비우기
  print(email); // null


  print("="*20);


  /// final : 값을 재할당 할 수 없음
  final String phone = "010-0000-0000";
  print(phone); // 010-0000-0000
  // phone = "010-1111-1111"; // final 때문에 이 코드는 실행 불가능
```

