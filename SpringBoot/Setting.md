# VS CODE에서 Spring Boot 환경 설치하기
## 1. 확장팩 설치하기
1. Java Extension Pack
![image](https://user-images.githubusercontent.com/30613069/172518450-1241e9d8-d652-4011-8264-85121fd37dc4.png)

2. Spring Boot Extension Pack
![image](https://user-images.githubusercontent.com/30613069/172518882-59ff7a0f-d7c1-4423-bbf2-4de001175da5.png)

3. Lombok Annotations Support for VS Code 
![image](https://user-images.githubusercontent.com/30613069/172519182-bb4fac22-7889-4c9f-9e85-14857664a2c3.png)

❗ ‘Spring Boot Tools’ 확장팩은 다음 파일 패턴을 가지는 파일에 대해서 파일수정할 때 활성화된다.
  - .java: 스프링 부트 사양을 따르는 경우(@SpringBoot 애너테이션과 main() 메서드가 함께있음) 활성화
  - application*.properties
  - application*.yml

다음 기능을 제공한다:
  - @RequiestMapping 에 선언된 경로(path)를 탐색할 수 있는 기능
  - 실행 중인 앱이 제공하는 경로에 접근할 수 있는 기능
  - 스프링 부트에 정의된 “Spring Boot Properties Metadata” 를 이용해서 .properties 와 .yml 에서 자동완성 및 검증기능을 제공

## 2. 프로젝트 생성
1. Ctrl + Shift + P 를 눌러 커맨드 팔레트(Command palette)를 열어 ‘Spring initalizr: Create a Gradle Project’ 를 선택한다.

2. Spring Boot version 선택: 2.7.3(2022-09-13 기준)
![image](https://user-images.githubusercontent.com/30613069/189904953-ee3b7f8c-54ee-4cd7-8d1d-7a1ac384b091.png)

3. Project language 선택: Java
![image](https://user-images.githubusercontent.com/30613069/189905099-3fb91404-994a-4f6c-bafd-d5dcd28ecce2.png)

4. Group Id 등록: com.example.hansol_wiki
![image](https://user-images.githubusercontent.com/30613069/189905200-c7d928eb-df0c-49d4-ab80-a8485b9ca988.png)

5. Artifact Id 등록: springboot_backend <- 폴더 이름?
![image](https://user-images.githubusercontent.com/30613069/189905570-2ed4a60f-3c23-4a7c-8469-2a01b1a5934d.png)

6. Packaging type 선택: JAR
![image](https://user-images.githubusercontent.com/30613069/189905646-753fe71a-fa99-4f3b-9c2f-b95efd78a475.png)

7. Java Version 선택: 11
![image](https://user-images.githubusercontent.com/30613069/189905717-e2f98ac3-eb4f-49d4-8bed-cd56029c9d14.png)

8. Dependnecies 선택(사용하려는 기술에 따라 다름)
- SpringWeb
![image](https://user-images.githubusercontent.com/30613069/189905897-e3f269e9-8148-48cf-9eb3-d0eb8a455e5a.png)

- jpa
![image](https://user-images.githubusercontent.com/30613069/189906030-55cfbfd6-2fdb-4097-9617-bd7c7a2dad05.png)

- lombok
![image](https://user-images.githubusercontent.com/30613069/189906154-7b7f980a-e767-4050-80d0-9587ae1599d2.png)

- mysql
![image](https://user-images.githubusercontent.com/30613069/189906261-fd1b8d80-34c3-479b-8fb4-282367b9038b.png)

9. 경로 선택
> spring-boot auth와 같은 경로에 무족건 있어야 된다고함
> 아직 난 생성을 안했으므로 만들어주겟음
![image](https://user-images.githubusercontent.com/30613069/189906751-98e7ec38-d37b-4cdf-9a04-b0c3d25b1bd1.png)

10. 완료
![image](https://user-images.githubusercontent.com/30613069/189907184-267b5c61-c805-4b46-a8c7-910240087293.png)



