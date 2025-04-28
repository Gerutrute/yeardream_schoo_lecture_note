# 소프트웨어 설계
- 소프트웨어를 어떻게 만들 것인가에 대한 구체적인 구조와 계획을 수립하는 단계
- 요구사항을 컴퓨터에서 어떻게 실현할 것인가를 결정하는 과정
- 설계 관점 : 관리적 시각, 기술적 시각
  관리적 시각에서의 설계 : 프로젝트 계획, 진척 관리, 자원 배분, 위험 관리 등 프로젝트 성공 지원에 초점 / 주요활동 : 기본설계 / 상세설계
  기술적 시각에서의 설계 : 실제 시스템 구현을 위한 기술적 요소 및 구조 설계에 초점 / 주요활동 : 자료설계 / UI 설계 / 구조 설계 / 설계 절차 설계

## 소프트웨어 설계의 분류
- 상위 설계, 하위 설계

  ![image](https://github.com/user-attachments/assets/336c22c9-f6d4-46de-b90a-284851455458)

### 설계의 원리
| 원리                     | 설명                                 |
| ------------------------ | ------------------------------------ |
| **단순성**               | 이해하기 좋은 구조                   |
| **효율성**               | 자원, 성능을 최적화하는 설계         |
| **구조화 (분할, 계층화)** | 체계적인 분할                        |
| **추상화**               | 불필요한 세부사항 감추기             |
| **모듈화**               | 독립적인 구성 요소로 나누기          |
| **정보 은닉**            | 내부 구현은 감추고, 외부 인터페이스만 공개 |

### 추상화
- 복잡한 시스템에서 핵심적인 정보만을 추려내고, 불필요한 세부사항은 감추는 것

  ![image](https://github.com/user-attachments/assets/9379f387-2d1b-4252-87fc-19a8498879e0)

### 모듈
- 전체 프로그램의 기능 중 특정 기능을 처리할 수 있는 실행 코드

  ![image](https://github.com/user-attachments/assets/57a397c0-73d6-41cf-ad4f-03f782f633e9)

### 결합도
- 모듈 간의 의존성 정도

  ![image](https://github.com/user-attachments/assets/209a9209-197c-491b-8f74-de9293c051ab)

### 응집도
- 모듈 내부 기능 간의 관련성 정도

  ![image](https://github.com/user-attachments/assets/382a6eb7-4d0b-4eb3-8555-50fe4777fd67)

* 좋은 모듈 예시

  ![image](https://github.com/user-attachments/assets/a2c909a3-605e-43ac-9ae4-5f6079a63714)

### 소프트웨어 설계 모델링
- 요구사항을 컴퓨터에서 어떻게 실현할 것인가를 결정하는 과정

  ![image](https://github.com/user-attachments/assets/0e695c25-d716-4957-85e2-24673fc0f5fa)

### 설계 모델의 구성

  ![image](https://github.com/user-attachments/assets/d8eeb259-8e88-4a19-a5d4-3ccdf1c3b4ff)

### 구조 모델링
- 시스템의 구성요소들 사이의 구조적 관계에 대한 특성을 표현한 모델링

  ![image](https://github.com/user-attachments/assets/ee40c6ea-049f-4466-a2f9-3bf9f84c2df5)

### 행위 모델링
- 시스템이나 객체가 시간 흐름에 따라 어떻게 반응하고 동작하는지 표현

  ![image](https://github.com/user-attachments/assets/bc6baeed-5954-49a7-801a-6ec4874e5e4f)

### 기능 모델링
- 시스템이 무엇을 해야하는지를 중심으로 표현한 모델

  ![image](https://github.com/user-attachments/assets/0b18daae-ea14-4e5a-83a4-2c270bd4f0ad)

## 구조적 설계
- 요구사항을 체계적으로 분석하고 모듈화하여 시스템 구조를 설계하는 접근 방식

### 구조적 방법론

  ![image](https://github.com/user-attachments/assets/8d2c1e44-8bf4-4f0f-8a2e-bdd61d583211)

### 자료 흐름도
- 시스템 내 정보 흐름을 시각적으로 표현

  ![image](https://github.com/user-attachments/assets/4eb8522d-4ab0-473d-a294-8f80f15be910)

  ![image](https://github.com/user-attachments/assets/25aea3f8-cf80-43d7-b1b3-43dfbaf7ccfc)

### 자료 사전
- 시스템에서 사용되는 모든 데이터의 정의를 체계적으로 기록하는 문서

  ![image](https://github.com/user-attachments/assets/49aee5ae-1c05-405c-8800-ef1c25956543)

### 소단위 명세서
- 세분화된 자료 흐름도에서 최하위 단계 프로세스 처리 절차를 설명한 것

  ![image](https://github.com/user-attachments/assets/fc362ea3-01e5-4735-b379-9bca696a4453)

### N-S chart
- 순차, 조건, 반복 구조를 직관적으로 표현하는 시각적 도구

  ![image](https://github.com/user-attachments/assets/83599242-0af0-4994-897c-f9a6927dc759)

### HIPO(Hierarchy + Input process output)
- 계층적 구조와 입력의 흐름을 표현하는 도구

  ![image](https://github.com/user-attachments/assets/795c2573-cd89-4327-a384-f9c785c4cc61)

### Dijkstra의 구조적 설계
- 제어 구조의 단순화 / 탑다운 설계 / 논리적 구조 증명

## 소프트웨어 아키텍처
- 주요 컴포넌트 사이의 인터페이스와 인터랙션을 포함한 시스템 구조의 설계 유형

### 소프트웨어 아키텍처의 정의
- 복잡한 개발을 체계적으로 접근하기 위한 밑그림

  ![image](https://github.com/user-attachments/assets/a49c827d-08f0-437f-a8a7-b2899a937e49)

### 소프트웨어 아키텍처의 개념

  ![image](https://github.com/user-attachments/assets/111748c9-9bb8-43fc-9bfe-b0c7ef996243)

### 소프트웨어 아키텍처의 특징

  ![image](https://github.com/user-attachments/assets/c4978fcd-5b60-4109-a341-12ba35c4c9e9)

### 소프트웨어 아키텍처 품질 속성

  ![image](https://github.com/user-attachments/assets/c2de0202-b961-448f-ab1b-7be422068408)

### 소프트웨어 아키텍처 패턴

  ![image](https://github.com/user-attachments/assets/fad69900-2f07-4973-a14e-ee941e36f1ff)

  ![image](https://github.com/user-attachments/assets/8b7a5819-fd0a-488c-93c4-ac06dfe06957)

### 계층구조
- 소프트웨어를 계층 단위로 나누는 패턴

  ![image](https://github.com/user-attachments/assets/8a6c8495-70d9-4d74-b1ed-c55fc6374677)

### MVC(Model / View / Controller)

  ![image](https://github.com/user-attachments/assets/d2839380-502e-464c-b3e4-ea38a8eb97e2)

### 클라이언트/서버
- 하나의 서버와 다수의 클라이언트로 구성되는 패턴

  ![image](https://github.com/user-attachments/assets/64d1525d-67fc-4fe5-a072-cd434f34695b)

### 파이프-필터
- 데이터 흐름을 생성하고 처리하는 시스템을 위한 구조

  ![image](https://github.com/user-attachments/assets/e73541ae-ac8a-4673-8332-9860e00ae16b)

### 내용 요약

# 소프트웨어 설계 요약



## 1️⃣ 소프트웨어 설계

소프트웨어 설계는
***\*요구사항을 기반으로 시스템을 어떻게 만들지 구체화하는 과정\****입니다.
개발 단계 중 설계는 ***\*요구사항과 구현 사이의 다리 역할\****을 하며,
시스템 구조, 데이터 처리 방식, 인터페이스 등을 정의합니다.

설계는 두 가지 시각으로 나뉩니다:

- ***\*관리적 시각\****: 전체 프로젝트 계획과 방향 설정
- ***\*기술적 시각\****: 실제 구현을 위한 기술적 구조 설계

또한, 설계는 범위에 따라 다음처럼 구분됩니다:

- ***\*상위 설계 (High-Level Design)\****: 시스템 전체 구조 중심
- ***\*하위 설계 (Low-Level Design)\****: 모듈 내부 동작 중심

이 둘이 유기적으로 연결돼야, 구현과 유지보수 모두 수월해집니다.



------

## 2️⃣구조적 설계

***\*구조적 설계\****는 기능 중심, 절차 중심으로 시스템을 구성하는 방식입니다.
***\*Top-down 방식\****으로 기능을 계층적으로 분해하고,
이를 시각화하고 문서화하기 위해 다양한 도구를 사용합니다.

주요 구성 요소 및 기법:

- `자료 흐름도 (DFD)`: 데이터 흐름과 처리 과정을 도식화
- `자료사전`: 시스템에서 사용하는 데이터 정의
- `소단위 명세서`: 각 프로세스의 상세 처리 절차
- `N-S 차트`: 순차, 조건, 반복 구조를 시각화
- `HIPO`: 계층적 기능과 입출력 구조를 함께 표현

이처럼 구조적 설계는 설계의 ***\*논리성과 일관성\****을 높이고,
***\*유지보수와 협업에 유리한 기반\****을 제공합니다.

------

## 3️⃣소프트웨어 아키텍처

소프트웨어 아키텍처는
***\*시스템 구성 요소들 사이의 관계를 체계적으로 표현하고\****,
전체 시스템의 큰 틀, 즉 ***\*골격을 만들어주는 역할\****을 합니다.
외부에서 바라봤을 때 어떤 기능이 있는지,
그 기능들이 어떻게 연결되어 있는지를 설명해줍니다.

아키텍처는 시스템 품질과도 밀접한 관계가 있습니다.
소프트웨어의 품질을 판단하는 3가지 기준:

- ***\*시스템 품질 속성\**** (보안, 성능 등)
- ***\*비즈니스 품질 속성\**** (출시 시기, 비용 등)
- ***\*아키텍처 품질 속성\**** (구조의 단순성, 유지보수성 등)

이 중 하나가 바로 아키텍처 품질이기 때문에,
***\*아키텍처 설계 자체가 소프트웨어 품질을 결정짓는 핵심 기준\****이 됩니다.

------

## 4️⃣ 아키텍처 패턴

***\*아키텍처 패턴\****은
반복적으로 나타나는 구조 문제에 대한 ***\*재사용 가능한 설계 해법\****입니다.
구조의 ***\*일관성\****, ***\*유지보수 용이성\****, ***\*재사용성\****을 높일 수 있고,
설계자 간 ***\*소통 도구\****로도 유용하게 사용됩니다.

대표적인 아키텍처 패턴:

- `계층 구조 패턴`: 기능을 층별로 나누어 독립성과 역할 분리
- `MVC`: 모델, 뷰, 컨트롤러로 역할을 나눠 유지보수에 유리
- `클라이언트 / 서버`: 요청–응답 구조, 데이터 중앙 관리에 효과적
- `파이프–필터`: 데이터를 여러 단계로 분리해 순차 처리

각 패턴은 상황에 따라 장단점이 다르기 때문에,
***\*시스템 특성에 맞게 선택하는 것이 중요\****합니다.
