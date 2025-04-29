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

### 정적 다이어그램
- 시스템의 정적인 부분을 가시화 하기 위하여 사용하는 다이어그램

  ![image](https://github.com/user-attachments/assets/20716f1e-5bbc-4a68-a4ce-58202aac9f82)

### 동적 다이어그램
- 시스템의 동적인 부분을 가시화 하기 위하여 사용하는 다이어그램

  ![image](https://github.com/user-attachments/assets/b8c5070a-b946-4edb-9c7f-c79d32791666)

## UML을 이용한 모델링
- 소프트웨어를 그림으로 설계하는 일

  ![image](https://github.com/user-attachments/assets/b5a04a54-e483-4f74-a95c-c08621796251)


### 요약

# 객체지향 설계 요약

## 1️⃣ 객체지향과 객체지향 프로그래밍

객체지향 프로그래밍(OOP)은
현실 세계의 사물이나 개념을 소프트웨어로 표현하는 방식입니다.
초기에는 절차 중심이었지만, 현재는 객체 중심 설계가 주류가 되었습니다.

### 객체(Object)란?

현실 세계에 존재하는 사람, 사물, 개념 등을 소프트웨어 안에서 표현한 단위입니다.
모든 객체는 고유한 정체성을 가지며, 자신의 상태를 나타내는 속성,
동작을 수행하는 메서드, 다른 객체와 상호작용하는 메세지를 가집니다.

### 객체(Object)의 주요 구성 요소

- 속성 (Attribute)
- 메서드 (Method)
- 메세지 (Message)

### 클래스(Class)와 인스턴스(Instance)

- 클래스: 객체를 만들기 위한 설계도
- 인스턴스: 클래스에서 실제로 만들어진 객체

클래스는 ‘설계도’, 객체는 ‘실체’, 인스턴스화는 클래스에서 객체를 생성하는 과정입니다.

------

## 2️⃣ 객체지향 프로그래밍의 특징

객체지향 프로그래밍은 4가지 주요 특성을 가집니다:

### 🔹 추상화 (Abstraction)

- 복잡한 정보 중 핵심만 추려내어 단순화
- 예: Car라는 추상 클래스 → Honda가 이를 상속받아 stop() 메서드 구현

### 🔹 캡슐화 (Encapsulation)

- 코드(메서드)와 데이터를 하나의 클래스에 묶고 외부에는 필요한 기능만 공개
- 예: 변수는 private, 접근은 getter/setter 메서드로만 허용

### 🔹 상속 (Inheritance)

- 부모 클래스의 속성과 기능을 자식 클래스가 물려받음
- 예: Vehicle → Car, Bus, Bike 등이 상속받아 기능 확장

### 🔹 다형성 (Polymorphism)

- 하나의 메서드가 다양한 방식으로 동작
- 예: start()를 호출했을 때 객체가 Car냐 Bike냐에 따라 다르게 반응

→ 컴파일 시간 다형성과 런타임 다형성이 있음

#### 오버로딩 (Overloading)

- ***\*동일한 이름의 메서드\****를 ***\*매개변수의 타입이나 개수\****를 달리하여 여러 개 정의하는 것
- 같은 클래스 내에서 정의되며, ***\*컴파일 시점에 결정됨\****

#### 오버라이딩 (Overriding)

- ***\*상속 관계\****에서 ***\*부모 클래스의 메서드를 자식 클래스가 재정의\****하는 것
- 메서드 이름, 매개변수, 반환형이 동일해야 하며, ***\*실행(런타임) 시점에 결정됨\****

------

## 3️⃣ 객체지향 설계 원칙 (SOLID 원칙)

유지보수성과 확장성을 고려한 객체지향 설계의 핵심 원칙입니다.

- ***\*SRP (단일 책임 원칙)\****: 클래스는 하나의 책임만 가져야 함
- ***\*OCP (개방-폐쇄 원칙)\****: 확장엔 열려 있고, 수정엔 닫혀 있어야 함
- ***\*LSP (리스코프 치환 원칙)\****: 자식 클래스는 부모를 대체할 수 있어야 함
- ***\*ISP (인터페이스 분리 원칙)\****: 불필요한 기능은 분리하여 작은 인터페이스로
- ***\*DIP (의존 역전 원칙)\****: 상위 모듈과 하위 모듈이 추상화(인터페이스)에 의존해야 함

→ DIP에서는 ***\*의존성 주입 (Dependency Injection)\****을 적극 활용

------

## 4️⃣ 객체지향 개발 방법론

OOP 설계를 체계적으로 수행하기 위한 대표적 방법론들이 있습니다:

- ***\*Booch\****: 클래스 구조를 시각적으로 표현, 다양한 관계성 강조
- ***\*OOSE\****: 유스케이스 중심, 요구사항과 사용자 시나리오 중심
- ***\*OMT\****: James Rumbaugh가 개발, 구조/행위/기능 모델로 나눠 분석
- ***\*Coad & Yourdon\****: E-R 다이어그램을 기반으로 개체 중심 표현

→ 대부분의 방법론은 UML의 등장으로 통합되어 발전함

------

## 5️⃣ UML 다이어그램

UML은 ***\*Unified Modeling Language\****의 약자로,
객체지향 시스템을 시각적으로 설계하기 위한 ***\*표준 모델링 언어\****입니다.

### 구성 요소:

- ***\*사물(Things)\****: 클래스, 객체, 활동 등 시스템을 구성하는 요소
- ***\*관계(Relationships)\****: 상속, 연관, 포함 등 사물 간의 연결
- ***\*다이어그램(Diagrams)\****: 시스템을 시각화하는 그림 도구

### 주요 다이어그램

#### 정적 다이어그램 (구조 중심)

- 클래스 다이어그램
- 객체 다이어그램
- 컴포넌트 다이어그램
- 배치 다이어그램

#### 행위 다이어그램 (행위 중심)

- 유스케이스 다이어그램
- 시퀀스 다이어그램
- 상태 다이어그램
- 활동 다이어그램

→ UML을 활용하면 ***\*시스템의 구조와 행위를 시각적으로 표현\****할 수 있습니다.
