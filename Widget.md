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

💡 버튼 클릭시 실행 순서는 다음과 같습니다.

1. 33번째 `print("3. 클릭 됨");` 출력
2. 37번째 number 1 증가
3. 36번째 라인의 `setState`로 인해 화면 갱신 (= build 함수 호출)
4. build 함수가 호출되어 23번째 `print("2. build 호출 됨");` 출력

💡 **StatefulWidget** 위젯에서 `setState()`를 호출하면 `build()` 함수가 다시 실행되면서 화면이 갱신됩니다.

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
        💡 Container는 Box 형태의 기본적인 위젯으로 다방면으로 많이 사용됩니다.
         
        ```dart
        Container(
          width: 200, // 폭
          height: 200, // 높이
          color: Colors.pinkAccent, // 박스 색상
          child: Text("I Love Flutter!"), // 자식 위젯
        ),
        ```
        
        - margin & padding & alignment
          
            💡 `margin` : 박스 바깥 영역
            `padding` : 박스 안쪽 영역
            `alignment` : child 정렬
            
            - **[[코드스니펫] DartPad margin & padding & alignment 학습](https://dartpad.dev/?id=eb20d38084c1ede129cab7bd98fa44e1&null_safety=true)**
              ![image](https://user-images.githubusercontent.com/30613069/172316141-e54fe131-5951-4657-9792-671b51e64467.png)

            💡 EdgeInsets 사용법
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
          
            💡 boxDecoration : Container의 테두리(border), 그림자, 색상 등을 꾸밀 때 사용합니다.
                - **[[코드스니펫] DartPad BoxDecoration 학습](https://dartpad.dev/?id=c68290f876ce3d711f32ce66f21b2868&null_safety=true)**
            ![image](https://user-images.githubusercontent.com/30613069/172316515-a2721303-a627-4e36-84ab-d6fee7bd8063.png)

            💡 아래와 같이 color와 decoration을 동시에 사용하면 에러가 나옵니다.
            
            ```json
            Container(
            	color: Colors.amber,
              decoration: BoxDecoration(),
            ),
            ```
            
            DartPad에서는 위 상황에서 애러 메세지가 안나오지만, 실제 VSCode에서 코딩할 때에는 `color와 decoration을 동시에 사용할 수 없습니다`고 에러 메세지가 나옵니다
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
    
      💡 URL로 된 이미지를 보여주는 방법을 배워보도록 하겠습니다.

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
