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
![image](https://user-images.githubusercontent.com/30613069/172089768-bbd5bec0-d08b-49d2-8d4a-e86155e232ed.png)
<BR/>

- List<T> 예시
```DART
void main() {
  // 배열 생성
  List<String> fruits = ["바나나"]; // 문자열만 담을 수 있는 배열을 생성합니다.
  print(fruits);
  print("fruits 개수 : ${fruits.length}"); // 개수 조회
  
-> 
[바나나]
fruits 개수 : 1

  // 추가
  print('--------- 추가 -----------');
  fruits.add('딸기'); // 딸기 추가
  print(fruits);
  
  fruits.add('배'); // 배 추가
  print(fruits);
  
  // fruits.add(1); // fruits 타입이 List<String>이므로 문자열만 추가 가능
  
-> 
[바나나, 딸기]
[바나나, 딸기, 배]

  // 조회
  print('--------- 조회 -----------');
  print(fruits[0]); // 배열에 0번째 원소 꺼내기
  print(fruits[1]); // 배열에 1번째 원소 꺼내기
  
->
바나나
딸기
  
  // 수정
  print('--------- 수정 -----------');
  print(fruits);
  fruits[0] = "키위"; // 0번째 바나나를 키위로 수정
  print(fruits);
  
->
[바나나, 딸기, 배]
[키위, 딸기, 배]
  
  // 삭제
  print('--------- 삭제 -----------');
  fruits.remove('딸기'); // 딸기와 일치하는 값이 제거됩니다.
  print(fruits);
  fruits.removeAt(0); // 0번째 원소 삭제
  print(fruits);
  
  ->
[키위, 배]
[배]

  // 뭐든지 담을 수 있는 배열 생성
  print('-------- dynamic --------');
  List<dynamic> buckets = [1, "문자", [1, 2]]; // dynamic은 모든 타입을 포괄합니다.
  print(buckets);
  buckets.add(true); // 아무거나 담을 수 있음
  print(buckets);
  print(buckets[2]); // 2번째 배열 조회
  print(buckets[2][0]); // 2번째 배열의 0번째 값 조회
-> 
[1, 문자, [1, 2]]
[1, 문자, [1, 2], true]
[1, 2]
1
}
```
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
  

- 흐름 제어문
  1) 조건문
  ```dart
  if (bool1) {
    // bool1이 **true**면 실행
  } else {
    // bool1이 **false**면 실행
  }
  ```
  - 조건문은 else if 형태로 계속해서 꼬리에 꼬리를 물 수 있습니다. 앞에서부터 하나 씩 비교해서 진행하면서 하나라도 true가 되어 실행되면, 뒤에 있는 조건문은 실행되지 않습니다.

	2) 반복문
	- 반복문은 특정한 코드를 반복해서 실행하도록 흐름을 제어하는 방법으로 FOR문 이라고 불리기도 합니다.
	```dart
	/// 💡 직접 입력하면 5줄을 작성해야 하지만,
	hello 1
	hello 2
	hello 3
	hello 4
	hello 5
	```
	
	```dart
	/// 반복문을 사용하면 3줄로 작성할 수 있습니다.
	for (int i = 0; i < 5; i++) {
	    print('hello ${i + 1}');
	}
	```
	
	 * 5줄이 아니라 100만줄이 되어도, 반복문을 사용하면 3줄만에 가능합니다 👍👍
	![image](https://user-images.githubusercontent.com/30613069/172138105-9f0d12cb-14b5-4c50-8265-46f40b135c84.png)

	
	3) 함수(Function)
	- 함수(function) 는 여러 코드를 묶어둔 상자입니다.
	![image](https://user-images.githubusercontent.com/30613069/172138130-484340d7-a9db-4ff3-aa11-e2601b810d23.png)

	


