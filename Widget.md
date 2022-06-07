# 1. Flutter Widget
- Flutter의 모든 위젯은 StatelessWidget 과 StatefulWidget으로 나뉨

  - StatelessWidget : 상태 변화가 없어 화면을 새로고침 할 필요가 없는 위젯
  - StatefulWidget : 상태 변화가 있어 화면을 새로고침 할 필요가 있는 위젯

## 1.1 StatelessWidget
1. StatelessWidget 생김새
- 실제 코드를 작성시 VSCode에서 모두 자동완성이 되기 때문에 코드를 외우실 필요는 전혀 없습니다! 구조와 실행 순서만 알기
![image](https://user-images.githubusercontent.com/30613069/172302341-d76b4505-8f70-41be-a41f-b62ae5d7170d.png)

- `extends StatelessWidget` : **StatelessWidget**의 기능을 물려받습니다.
- `생성자` : 클래스 이름과 동일한 함수
- `build 함수` : 화면에 보여줄 자식 위젯을 반환

https://dartpad.dev/?id=847e8f2ade70953666b461e745d8686f&null_safety=true
![image](https://user-images.githubusercontent.com/30613069/172303431-0f1f13f4-3b63-4bf4-83fc-e542dd83cafb.png)
- 8번째 줄에 MyApp 클래스가 직접 만든 StatelessWidget 위젯입니다.
![image](https://user-images.githubusercontent.com/30613069/172303470-dacac786-6520-4aa5-ba70-1c2061b6948f.png)

```dart
import 'package:flutter/material.dart'; // Material 위젯 가져오기

void main() {
  print("1. 시작");
  runApp(const MyApp()); // MyApp 위젯으로 Flutter 시작!
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    print("2. build 호출 됨");
    
    // 화면에 보여지는 영역
    return const MaterialApp(
      home: Scaffold(
        body: Center(
          child: Text(
            "hello Stateless Widget",
            style: TextStyle(fontSize: 35),
          ),
        ),
      ),
    );
  }
}
```

## 1.2 StatefulWidget
1. StatefulWidget
- 기본적으로 2개의 클래스로 구성되어 있음!
![image](https://user-images.githubusercontent.com/30613069/172304018-21e231e8-62ed-49e3-84ac-058c913575e2.png)

- `MyApp` : **StatefulWidget**의 기능을 물려받 클래스
- `_MyAppState` : `MyApp` 상태를 가진 클래스(실질적인 내용은 여기에 들어가요!)
![image](https://user-images.githubusercontent.com/30613069/172304431-f51074e0-c407-401e-a783-94cb71e1706f.png)
- 화면을 그리는 build 함수는 상태 클래스에 있습니다.

https://dartpad.dev/?id=dd2dbb0f5f660469e8ca32f2434b3275&null_safety=true
![image](https://user-images.githubusercontent.com/30613069/172304627-d849328c-7ce8-4809-9c6d-db7148ba667d.png)

```dart
// ignore_for_file: prefer_const_constructors
import 'package:flutter/material.dart'; // Material 위젯 가져오기

void main() {
  print("1. 시작");
  runApp(const MyApp()); // MyApp 위젯으로 Flutter 시작!
}

// StatefulWidget의 기능을 물려받음
class MyApp extends StatefulWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  State<MyApp> createState() => _MyAppState();
}

// MyApp의 상태를 나타내는 클래스
class _MyAppState extends State<MyApp> {
  int number = 1; // number가 1인 상태

  @override
  Widget build(BuildContext context) {
    print("2. build 호출 됨");

    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: Text("$number", style: TextStyle(fontSize: 35)),
        ),
        floatingActionButton: FloatingActionButton(
          child: Icon(Icons.add),
          onPressed: () {
            print("3. 클릭 됨");

            // setState : build 메소드를 다시 호출해서 화면 갱신!
            setState(() {
              number += 1; // number를 1만큼 증가
            });
          },
        ),
      ),
    );
  }
}
```

> 💡 버튼 클릭시 실행 순서는 다음과 같습니다.
>
> 1. 33번째 `print("3. 클릭 됨");` 출력
> 2. 37번째 number 1 증가
> 3. 36번째 라인의 `setState`로 인해 화면 갱신 (= build 함수 호출)
> 4. build 함수가 호출되어 23번째 `print("2. build 호출 됨");` 출력
>
> 💡 **StatefulWidget** 위젯에서 `setState()`를 호출하면 `build()` 함수가 다시 실행되면서 화면이 갱신됩니다.

# 2. 화면을 만드는 데 필요한 기능
## 2.1 화면 그리기
- 원하는 위치에 원하는 요소를 배치하는 작업을 레이아웃(layout)이라 칭함

## 2.2 기본 위젯
- TEXT
- 기본 위젯
    - Text
       - **[[코드스니펫] DartPad Text Widget 학습](https://dartpad.dev/?id=d4af51e0a510ac4dd9a12a41f8276f3c&null_safety=true)**
                
        ```dart
        Text(
          '텍스트 위젯',
          style: TextStyle(
            fontSize: 35, // 폰트 크기
            fontWeight: FontWeight.bold, // 폰트 두께
            color: Colors.amber, // 폰트 색상
          ),
        ),
        ```
        
    - Container
      > 💡 Container는 Box 형태의 기본적인 위젯으로 다방면으로 많이 사용됩니다.
         
        ```dart
        Container(
          width: 200, // 폭
          height: 200, // 높이
          color: Colors.pinkAccent, // 박스 색상
          child: Text("I Love Flutter!"), // 자식 위젯
        ),
        ```
        
        - margin & padding & alignment
          > 💡 `margin` : 박스 바깥 영역
          >  `padding` : 박스 안쪽 영역
          >  `alignment` : child 정렬
            
            - **[[코드스니펫] DartPad margin & padding & alignment 학습](https://dartpad.dev/?id=eb20d38084c1ede129cab7bd98fa44e1&null_safety=true)**
              ![image](https://user-images.githubusercontent.com/30613069/172316141-e54fe131-5951-4657-9792-671b51e64467.png)
<br/>

- 💡 EdgeInsets 사용법
![image](https://user-images.githubusercontent.com/30613069/172316318-0257eeb2-fe20-4eac-9e50-455c45c8d210.png)

  - 전방위 모두 동일하게 적용

  ```dart
  EdgeInsets.all(8)
  ```

  - 특정 방위만 적용

    ```dart
    EdgeInsets.only(
      left: 8,
      right: 8,
    )
    ```

  - 위아래 또는 좌우 적용

    ```dart
    EdgeInsets.symmetric(
      vertical: 8,
      horizontal: 8,
    )
    ```

  - boxDecoration
    > 💡 boxDecoration : Container의 테두리(border), 그림자, 색상 등을 꾸밀 때 사용합니다.
    - **[[코드스니펫] DartPad BoxDecoration 학습](https://dartpad.dev/?id=c68290f876ce3d711f32ce66f21b2868&null_safety=true)**
    ![image](https://user-images.githubusercontent.com/30613069/172316515-a2721303-a627-4e36-84ab-d6fee7bd8063.png)

    > 💡 아래와 같이 color와 decoration을 동시에 사용하면 에러가 나옵니다.

    ```json
    Container(
      color: Colors.amber,
      decoration: BoxDecoration(),
    ),
    ```

> DartPad에서는 위 상황에서 애러 메세지가 안나오지만, 실제 VSCode에서 코딩할 때에는 `color와 decoration을 동시에 사용할 수 없습니다`고 에러 메세지가 나옵니다
![image](https://user-images.githubusercontent.com/30613069/172316584-a15d4591-fd35-4e82-818f-215eb868d431.png)

* 에러가 나지않게 하려면 아래와 같이 color를 decoration 안에 넣으면 됩니다.

```json
Container(
  decoration: BoxDecoration(
    color: Colors.amber,
  ),
),
```      
    - Icon
          - [**[코드스니펫] DartPad Icon 학습**](https://dartpad.dev/?id=c9873d52cdf3902fd378b49346fad894&null_safety=true)
          ![image](https://user-images.githubusercontent.com/30613069/172317525-66f760d8-f6c2-474c-bbc0-811e7ec74f1a.png)

          - Material Icon
            
            ```dart
            import 'package:flutter/material.dart';
            
            Icon(
              Icons.home,
              color: Colors.blue,
              size: 50,
            ),
            ```
            
          - Cupertino Icon
            
            ```dart
            import 'package:flutter/cupertino.dart';
            
            Icon(
              CupertinoIcons.house,
              color: Colors.pink,
              size: 50,
            ),
            ```

        💡 아래 링크는 Material과 Cupertino 아이콘들을 한 눈에 볼 수 있는 사이트입니다. 이름만 확인하시면 코드에서 바로 사용하실 수 있습니다.
        
        - [**[코드스니펫] Material Icon 모아보기 URL**](https://fonts.google.com/icons?selected=Material+Icons)

        - [**[코드스니펫] Cupertino Icon 모아보기 URL**](https://shuuji3.xyz/flutter-packages/third_party/packages/cupertino_icons/)
        
    - Image
      > 💡 URL로 된 이미지를 보여주는 방법을 배워보도록 하겠습니다.

      - [**[코드스니펫] DartPad Image.network 학습**](https://dartpad.dev/?id=59351b15e43e1abc08c5e4b4945bd5b1&null_safety=true)
             
        💡 18번째 줄의 `Image.network("URL")`과 같이 사용할 수 있습니다.
        ![image](https://user-images.githubusercontent.com/30613069/172317668-d1920a7f-3bb1-4ccc-8123-691f15e25f0a.png)

     - 레이아웃(Layout) 위젯
      - Scaffold
        > 건물을 지을 때 공사장에 먼저 비계(Scaffold)를 설치하고 작업을 시작합니다.
        > 앱에서도 화면을 그릴 때 Scaffold 위젯으로 시작합니다.
        > Scaffold 위젯은 한 페이지의 레이어를 쉽게 구성할 수 있도록 틀을 잡아줍니다.

        ```dart
        Scaffold(
          appBar: AppBar(), // 상단 바
          body: Text(), //화면 중앙에 가장 큰 면적
          bottomNavigationBar: BottomNavigationBar(), //하단 바
          floatingActionButton: FloatingActionButton(), //우측 하단
        ),
        ```
        ![image](https://user-images.githubusercontent.com/30613069/172320996-d87f926e-ed80-446e-a598-571642982e95.png)

      - [**[코드스니펫] DartPad Scaffold 학습**](https://dartpad.dev/?id=2f4c9219451f3d6632b8c0781bb850d1&null_safety=true)
        ![image](https://user-images.githubusercontent.com/30613069/172322671-ea95f334-4e67-451f-bf6e-7ef1e2d385fa.png)

        - appBar
          > 💡 AppBar는 앱의 상단 영역을 의미합니다.
          >  상단에 파란색 영역이 바로 AppBar 영역입니다.
          ![image](https://user-images.githubusercontent.com/30613069/172322921-2e98dcdf-0e4f-46a4-8989-55ca020c4930.png)
          
          > AppBar에 `title`을 넣어 보겠습니다. 코드스니펫을 복사해서 밑에 이미지처럼 `AppBar()` 소괄호 사이에 붙여넣어 볼게요!
          ![image](https://user-images.githubusercontent.com/30613069/172323024-aa0d71aa-a411-45db-80fc-b3f596952994.png)

        - body
        > 💡 body는 화면에 가장 넓은 면적을 차지합니다.
        >  Body에 Container 위젯을 추가해볼게요.
          ```dart
          body: Container(width: 200, height: 200, color: Colors.amber),
          ```
        ![image](https://user-images.githubusercontent.com/30613069/172323893-86100e3e-912c-46d9-a495-71f1f1531b15.png)
         
        > 💡 Container는 박스 모양의 상자 위젯 입니다.
        
        ** Dart 줄 정렬 팁 하나 알고 진행할게요!**
        1. 17번째 라인 `Colors.amber` 뒤에 `쉼표(,)`를 추가한 뒤 상단에 `Format` 버튼을 눌러볼게요.
        ![image](https://user-images.githubusercontent.com/30613069/172324454-837feb65-ad57-4a02-aefb-564eca2a5344.png)
        
        > 그러면 body의 Container 속성이 한 줄로 보기 좋게 정렬이 됩니다.
        > 💡 Dart는 쉼표를 기준으로 코드를 자동 정렬해 줍니다.
        > 가능한 코드 마지막 부분에 쉼표를 항상 넣어주는 습관을 들이면 좋습니다.
        ![image](https://user-images.githubusercontent.com/30613069/172324639-3e656443-4e6b-4da9-9272-383be881c5e3.png)  
        
        2. `Container` 위젯을 body 전체를 가득 채우도록 만들어볼게요. 코드 스니펫을 복사해서 `Container`의 `width`와 `height`의 값 `200`을 변경해주세요.
        - **[코드스니펫] Container size**
          ```dart
          double.infinity
          ```
        > 그러면 Container가 body를 가득 채우게 됩니다.
          ![image](https://user-images.githubusercontent.com/30613069/172324896-dd6b46b4-954f-4cb9-94aa-85f063d94da5.png)

        - bottomNavigationBar
          > 💡 bottomNavigationBar는 가장 하단에 위치해 있습니다.
          > 아래 코드스니펫을 복사해서 21번째 라인 맨 뒤를 클릭한 뒤에 붙여 넣을게요.
            ```dart
                    bottomNavigationBar: BottomNavigationBar(
                      items: const <BottomNavigationBarItem>[
                        BottomNavigationBarItem(
                          icon: Icon(Icons.alarm),
                          label: 'Alarm',
                        ),
                        BottomNavigationBarItem(
                          icon: Icon(Icons.nightlight_round),
                          label: 'Sleep',
                        ),
                        BottomNavigationBarItem(
                          icon: Icon(Icons.settings),
                          label: 'Setting',
                        ),
                      ],
                      currentIndex: 0, // 현재 선택된 메뉴
                      selectedItemColor: Colors.amber,
                    ),
            ```

          > 💡 `BottomNavigationBar` 위젯을 이용하면 아래와 같은 하단 레이어를 만들 수 있습니다. 좀 더 상세한 내용은 [공식 문서](https://api.flutter.dev/flutter/material/BottomNavigationBar-class.html)를 참고해주세요.
          > 
          > items : 각각의 메뉴 버튼들이 모여있는 배열(List)
          > currentIndex : 현재 선택된 items의 index
          ![image](https://user-images.githubusercontent.com/30613069/172325341-a6d96e6a-f032-4501-ba2e-978b5ce870a3.png)

        - floatingActionButton
          > 💡 floatingActionButton은 사용자가 가장 누르기 쉬운 위치인 우측 하단에 있습니다.
          > 39번째 라인 맨 뒤를 클릭한 뒤, 아래 코드스니펫을 붙여 넣어 줍니다.
          ```dart

                  floatingActionButton: FloatingActionButton(
                    onPressed: () {
                      print("클릭 되었습니다!");
                    },
                    child: const Icon(
                      Icons.add,
                      color: Colors.amber,
                    ),
                    backgroundColor: Colors.white,
                  ),
          ````
          ![image](https://user-images.githubusercontent.com/30613069/172326277-aff819d1-fdb7-4afe-af4d-38b0666d3444.png)

          > 클릭 이벤트가 수신 되는 부분은 42번째 라인에 `onPressed` 부분입니다.
          > 💡 onPressed는 익명함수(이름이 없는 함수)를 전달 받고, 내부적으로 클릭이 되었을 때 해당 익명함수를 호출해주는 방식으로 동작합니다.

          ```dart
          onPressed: () {
            print("클릭 되었습니다!");
          },
          ```

-> 💡 `Scaffold` 위젯은 위에서 소개해드린 기능 이외에도 더 많은 기능들을 가지고 있습니다. 더 자세히 알고 싶으신 분은 공식문서 또는 `flutter scaffold`로 검색하여 찾을 수 있습니다.

- **[[코드스니펫] Scaffold 공식문서 URL](https://api.flutter.dev/flutter/material/Scaffold-class.html)**

        - Column
          > 💡 Column 위젯은 세로 방향에 대한 레이아웃을 잡을 때 사용합니다.
          ```dart
          Column(
            children: [ // 자식 위젯들
              Text("위젯1"),
              Text("위젯2"),
            ],
          ),
          ```

          - mainAxisSize : 세로 방향에 대한 크기
            - [**[코드스니펫] DartPad MainAxisSize 학습**](https://dartpad.dev/?id=185f5ce90c9cb1b4a8df349be0d44f03&null_safety=true)

                      ```dart
                      https://dartpad.dev/?id=185f5ce90c9cb1b4a8df349be0d44f03&null_safety=true
                      ```


              ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9c0ea154-0069-4ae0-9967-e236a0b37242/Untitled.png)

          - mainAxisAlignment : 세로 방향에 대한 정렬
              - 코드스니펫을 복사한 뒤 주소창에 붙여 넣으면, DartPad로 접속합니다.
                  - **[[코드스니펫] DartPad MainAxisAlignment 학습](https://dartpad.dev/?id=32012b45f94329c182cb5a786051c3df&null_safety=true)**

                      ```dart
                      https://dartpad.dev/?id=32012b45f94329c182cb5a786051c3df&null_safety=true
                      ```


              ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/73bf69ec-0716-471b-ab40-7a910f75bb6a/Untitled.png)

          - crossAxisAlignment : 가로 방향에 대한 정렬
              - 코드스니펫을 복사한 뒤 주소창에 붙여 넣으면, DartPad로 접속합니다.
                  - **[[코드스니펫] DartPad CrossAxisAlignment학습](https://dartpad.dev/?id=189116b5051c3c25ebae5abf0280650c&null_safety=true)**

                      ```dart
                      https://dartpad.dev/?id=189116b5051c3c25ebae5abf0280650c&null_safety=true
                      ```


              ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/adc0d123-0551-4179-9bd1-a0290ac4ec68/Untitled.png)

      - Row

          <aside>
          💡  Column에서 가로 세로 방향만 바꾸면 Row이므로 넘어갈게요!

          </aside>

          - mainAxisAlignment : 가로 방향에 대한 정렬
          - crossAxisAlignment : 세로 방향에 대한 정렬
      - Stack

          <aside>
          💡 화면에 위젯을 쌓고 싶을 때 사용하는 위젯입니다.

          </aside>

          ```dart
          Stack(
            children: [ // 자식 위젯들
              Text("위젯1"),
              Text("위젯2"),
            ],
          ),
          ```

          - 코드스니펫을 복사한 뒤 주소창에 붙여 넣으면, DartPad로 접속합니다.
              - [**[코드스니펫] DartPad Stack 학습**](https://dartpad.dev/?id=357a036ace4a11adbaca8922a434c676&null_safety=true)

                  ```dart
                  https://dartpad.dev/?id=357a036ace4a11adbaca8922a434c676&null_safety=true
                  ```

              - `children`에서 아래에 있는 위젯이 더 위에 표시됩니다.
              - `alignment`를 이용해서 자식 위젯들을 이동할 수 있어요.

              ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6401c71d-2622-4e37-9b0e-c6a9c2b8b774/Untitled.png)

          - 코드스니펫을 복사한 뒤 주소창에 붙여 넣으면, DartPad로 접속합니다.
              - **[[코드스니펫] DartPad Positioned 위젯 학습](https://dartpad.dev/?id=7f644765fa450e5c7e71da549db64b68&null_safety=true)**

                  ```dart
                  https://dartpad.dev/?id=7f644765fa450e5c7e71da549db64b68&null_safety=true
                  ```

              - `Positioned` 위젯을 이용하면 Stack 내부에서 원하는 위치에 배치할 수 있습니다.

              ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3e042004-7e99-41ec-a6f8-87cb1b2941b2/Untitled.png)

      - SingleChildScrollView

          <aside>
          💡 **SingleChildScrollView**는 Child 위젯이 화면의 스크린보다 큰 경우, 스크롤 할 수 있도록 만들어줍니다.

          </aside>

          ```dart
          SingleChildScrollView(
            child: Container(height: 10000), // 자식 위젯
          ),
          ```

          - 코드스니펫을 복사한 뒤 주소창에 붙여 넣으면, DartPad로 접속합니다.
              - [**[코드스니펫] DartPad SingleChildScrollView 학습**](https://dartpad.dev/?id=5ac9fd613161a8c09c7946bd57c627a3&null_safety=true)

                  ```dart
                  https://dartpad.dev/?id=5ac9fd613161a8c09c7946bd57c627a3&null_safety=true
                  ```

              - `Column`의 자식 위젯들의 높이의 총 합이 화면의 높이보다 큰 경우 `SingleChildScrollView`로 감싸주어 스크롤을 할 수 있도록 만들어 줍니다.

              ![scroll.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/aa3cd791-bf7d-4bde-953b-f0d48072d473/scroll.png)

          - SingleChildScrollView를 제거해 봅시다.

              `SingleChildScrollView`를 클릭한 뒤 `alt + Enter`를 누르면 아래와 같은 창이 뜹니다. 여기서 `Remove this widget`을 선택해서 위젯을 삭제한 뒤 `Run` 버튼을 눌러주세요.

              ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/db5bd73c-7b05-44c6-a355-3460b46315e6/Untitled.png)

          - 위젯이 너무 커서 흘러 넘치는(Overflow) 되는 경우, 화면 상에 아래와 같이 표시됩니다.

              ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ed5cadef-629f-48e5-877c-bc94a4d16e3c/Untitled.png)

          - 다시 `Column` 위젯을 `SingleChildScrollView`로 감싸주도록 하겠습니다. `Column` 위젯을 선택한 뒤 `alt + Enter`를 누른 뒤 `Wrap with Widget...`을 선택해 주세요.

              ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a9616834-3be9-41fa-87c2-90a25fdf7ead/Untitled.png)

              그러면 아래와 같이 `widget`이 `Column`을 감싸게 됩니다.

              ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e2dcf8e7-a554-4864-9cfd-bac53f922d82/Untitled.png)

              `widget`을 `SingleChildScrollView`로 변경한 뒤 `Run` 버튼을 누르면 다시 스크롤이 됩니다.

              ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/496e64a3-a16f-49f9-9e07-8166ce886f0b/Untitled.png)

  - 2) 텍스트 입력 받기

      <aside>
      💡 Flutter에서 텍스트 입력을 받을 때 **`TextField`** 위젯을 사용합니다.

      </aside>

      ```dart
      TextField(
        autofocus: true, // 자동 포커스
        onChanged: (text) {
          // 텍스트 변경시 실행되는 함수
        },
        onSubmitted: (text) {
          // Enter를 누를 때 실행되는 함수
        },
      ),
      ```

      - 코드스니펫을 복사한 뒤 주소창에 붙여 넣으면, DartPad로 접속합니다.
          - [**[코드스니펫] DartPad TextField 학습**](https://dartpad.dev/?id=5a36ad5c83cc90dfe9260dd648f5a958&null_safety=true)

              ```dart
              https://dartpad.dev/?id=5a36ad5c83cc90dfe9260dd648f5a958&null_safety=true
              ```

      - `autofocus` : 해당 위젯이 화면에 보일 때 바로 포커스 되는지의 여부
      - `onChanged` : 텍스트 변경 시 현재 입력된 값이 파라미터로 넘어오는 함수
      - `onSubmitted` : Enter를 누르는 경우 현재 입력된 값이 파라미터로 넘어오는 함수

      ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/838a7394-54eb-4c17-ab3d-a5b02bf23260/Untitled.png)

  - 3) 클릭 이벤트 받기

      <aside>
      💡 Flutter는 클릭 이벤트를 받는 다양한 Button을 제공합니다.

      </aside>

      ```dart
      // 위로 올라와 있는 듯한 버튼
      ElevatedButton(
        onPressed: () {
          print("Elevated Button 클릭");
        },
        child: Text('Elevated Button'),
      ),

      // 텍스트 버튼
      TextButton(
        onPressed: () {
          print("Text Button 클릭");
        },
        child: Text('Text Button'),
      ),

      // 아이콘 버튼
      IconButton(
        onPressed: () {
          print("Icon Button 클릭");
        },
        icon: Icon(Icons.add),
      ),
      ```

      - 코드스니펫을 복사한 뒤 주소창에 붙여 넣으면, DartPad로 접속합니다.
          - [**[코드스니펫] DartPad Button 학습**](https://dartpad.dev/?id=a021433e7a40365152e52f150d0e46ed&null_safety=true)

              ```dart
              https://dartpad.dev/?id=a021433e7a40365152e52f150d0e46ed&null_safety=true
              ```

      - `ElevatedButton` : 위로 올라와 있는 듯한 버튼
      - `TextButton` : 텍스트 버튼
      - `IconButton` : 아이콘 버튼

      ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/49686f8f-ba27-417a-8b2a-bb203c886f77/Untitled.png)

  - 4) 화면 이동

      <aside>
      💡 Flutter에서 각 화면을 라우트(Route)라고 부르며, 화면을 이동할 때 `네비게이터(Navigator)`를 사용합니다.

      </aside>

      - 다음 페이지로 이동하기

          ```dart
          Navigator.push(
            context,
            MaterialPageRoute(builder: (context) => SecondPage()), // 이동하려는 페이지
          );
          ```

      - 현재 화면 종료

          ```dart
          Navigator.pop(context); // 종료
          ```

      - 코드스니펫을 복사한 뒤 주소창에 붙여 넣으면, DartPad로 접속합니다.
          - [**[코드스니펫] DartPad Routing 학습**](https://dartpad.dev/?id=980f8328245093313b950135fd63979a&null_safety=true)

              ```dart
              https://dartpad.dev/?id=980f8328245093313b950135fd63979a&null_safety=true
              ```


          ![Routing.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0d93233f-58cb-448a-bb05-7b6f4aa6c438/Routing.png)


      <aside>
      💡 화면이 많아지는 경우, [Named Route](https://docs.flutter.dev/cookbook/navigation/named-routes) 방식을 사용하기도 합니다.

      </aside>
