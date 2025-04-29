# 소프트웨어 설계 기법

  ![image](https://github.com/user-attachments/assets/a389afae-8736-4851-85c3-ed3ae7327c61)

## 객체 지향 프로그래밍

  ![image](https://github.com/user-attachments/assets/4164744c-429e-4fab-b1a2-a746348b7376)

### 객체
- 현실 세계의 사물이나 개념을 소프트웨어로 표현한 것

  ![image](https://github.com/user-attachments/assets/81cf9f6a-310c-432a-ada0-d0250615de4e)

### 클래스
- 객체를 만들기 위한 설계도 또는 틀

  ![image](https://github.com/user-attachments/assets/ae9dd6b5-ecdf-4389-8cae-51e7b3968bc2)

  ![image](https://github.com/user-attachments/assets/c86c71ea-9e5c-46f1-a370-05867be413d9)

### 객체지향 프로그래밍 특징

  ![image](https://github.com/user-attachments/assets/bf6b151d-e6b1-4885-a450-500a399a8dbf)

### 추상화
- 구현 세부사항은 숨기고 사용자에게는 기능만 보여주는 과정

  ![image](https://github.com/user-attachments/assets/80e42519-f945-4206-b37e-cf3256ce7ac5)

  추상화 예시 : https://colab.research.google.com/drive/1rga9xAaSU70VtjY3P3g4Sq5-ZY2OIby9

### 캡슐화
- 코드와 데이터를 하나의 단위(클래스)로 묶는 과정

  ![image](https://github.com/user-attachments/assets/16e33e6b-2914-414a-8929-8579b1049810)

### 상속성
- 기존에 잘 만든 클래스를 기반으로 새로운 클래스를 만드는 방법
  
  ![image](https://github.com/user-attachments/assets/ab8fd5f1-ced6-4bde-b58c-98ed25e007fd)

### 다형성
- 여러가지 형태를 가질 수 있는 능력
  
  ![image](https://github.com/user-attachments/assets/eca2447a-4de7-4aa0-86b5-ed42f1ec3572)

  ![image](https://github.com/user-attachments/assets/20c79767-a7f8-4379-bd8d-c50e7663e383)

### 오버로딩과 오버라이딩
- 객체지향의 핵심 특성 중 하나인 다형성을 구현하기 위한 기술

  ![image](https://github.com/user-attachments/assets/6a195c95-bfca-432d-9a5b-37081ed49aec)

### 객체지향 기법
- 객체지향 기법에서 객체들 사이의 관계성을 나타내는 방법

|                    | Association (연관)           | Aggregation (집합)           | Composition (합성)             |
|--------------------|------------------------------|------------------------------|--------------------------------|
| **관계 예시**       | Teacher — Student            | School ◌—— Student           | House ♦—— Room                 |
| **특징**           | • 일반적인 관계<br>• 전체 간 연결만 있을 뿐, 포함하지 않음<br>• 생명 주기는 서로 독립적 | • 포함 관계<br>• 생명 주기는 독립적<br>• 전체가 사라져도 부분 개체는 사라지지 않음 | • 강한 포함<br>• 생명 주기는 의존적<br>• 한 객체가 없어진다면 포함된 객체도 없어짐 |


## SOLID 원칙
- 변경에 강하고 유지보수가 쉬운 설계를 위한 원칙

  ![image](https://github.com/user-attachments/assets/ef9550ad-3ee5-4659-bc3c-4876930a06f2)

### 단일 책임 원칙
- 클래스는 단 하나의 책임만 가져야 한다.

  ![image](https://github.com/user-attachments/assets/64002939-4fbb-4fd2-9a89-022ee606ffc5)

### 개방-폐쇄 원칙
- 확장에는 열려있고 수정에는 닫혀 있어야함

  ![image](https://github.com/user-attachments/assets/676499bf-d375-47ed-8002-5a15fe3dbce2)

### 리스코프 치환 원칙
- 상속에 대한 원칙

  ![image](https://github.com/user-attachments/assets/d4e9b814-f79b-4ab4-9452-def0ad73a4e4)

### 인터페이스 분리 원칙
- 단일 역할 인터페이스 설계

  ![image](https://github.com/user-attachments/assets/8d70446d-2a8b-4c14-9829-cffbc46bc3cd)

### 의존 역전 원칙
- 설계 방향은 구현이 아니라 추상에 맞추기

  ![image](https://github.com/user-attachments/assets/df647df8-0d95-432d-a5bc-2a53edee48de)

# 객체지향 개발 방법론
- 객체지향 개발을 체계적으로 수행하기 위한 절차적 접근

  ![image](https://github.com/user-attachments/assets/fdfab22f-4807-4e85-bf49-12766b6b9af2)

## BOOCH 방법론
- 다양한 다이어그램을 통해 시스템의 구조와 동작을 시각화하는 방법론

  ![image](https://github.com/user-attachments/assets/8c0c9d64-c12d-42ca-8c65-06e5752895c7)

## OOSE
- Use Case 개념을 처음 도입한 방법론

  ![image](https://github.com/user-attachments/assets/5cda8c48-7c3e-439a-96b6-2674a2154e99)

## OMT
- 개발 과정을 세 가지 모델로 나누어 체계적으로 접근

  ![image](https://github.com/user-attachments/assets/311f75e8-0751-46a1-8fce-9fe78224fcb9)

  ![image](https://github.com/user-attachments/assets/a4235fd2-95e7-4a1a-aeae-558ea4ba451f)

  ![image](https://github.com/user-attachments/assets/2e8ad073-da5c-4c21-8a4f-088837a8dc14)

  ![image](https://github.com/user-attachments/assets/4eabaf6d-9c42-4a13-86cf-97a8e29b3187)

## Coad & Yourdon 방법론
- E-R 다이어그램으로 객체의 행위를 모델링하는데 초점을 둔 방법

  ![image](https://github.com/user-attachments/assets/b837512c-cc5d-466e-8145-5b7167f5346d)

## UML의 정의
- 소프트웨어 시스템을 시작적으로 모델링(설계)하기 위한 표준화된 언어

  ![image](https://github.com/user-attachments/assets/ba86d6e2-3042-42f0-a91a-ad4547e5da5c)

## UML의 구성요소

  ![image](https://github.com/user-attachments/assets/74e4edec-6e60-4099-a58e-008b5fc01b42)

### UML의 구성요소 - 사물
- 모델 안에서 존재하거나 다루어지는 요소들

  ![image](https://github.com/user-attachments/assets/91717add-7d9e-4fcb-bb02-55141b59953f)

### UML의 구성요소 - 관계
- 사물 간의 연결관계를 추상화하여 표현한 것

  ![image](https://github.com/user-attachments/assets/230e0964-6806-4e35-906c-2473bdc7e180)

### UML의 구성요소 - 다이어그램
- 사물들 간의 관계를 도형으로 보여준 것

  ![image](https://github.com/user-attachments/assets/928de746-3baf-440a-bd05-e3ca8a36a892)

## UML을 이용한 모델링
- 소프트웨어를 그림으로 설계하는 일

  ![image](https://github.com/user-attachments/assets/b5a04a54-e483-4f74-a95c-c08621796251)

