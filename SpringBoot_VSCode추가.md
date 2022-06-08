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
2. Spring Boot version 선택: 2.7.0(2022-06-08 기준)
3. Project language 선택: Java
4. Group Id 등록: com.example.hansol_wiki
5. Artifact Id 등록: springboot_backend
6. Packaging type 선택: JAR
7. Java Version 선택: 11

Dependnecies 선택(사용하려는 기술에 따라 다름)
![image](https://user-images.githubusercontent.com/30613069/172520938-826b5b54-9588-472c-9545-91f4baf0ae74.png)

Spring Boot DevTools
Lombok
Spring Configuration Processor
Spring Web
Spring Data JPA
H2 Database
Flyway Migration
MariaDB Driver

![image](https://user-images.githubusercontent.com/30613069/172521447-c8162b10-79f6-4534-93df-8e2485cb4977.png)

