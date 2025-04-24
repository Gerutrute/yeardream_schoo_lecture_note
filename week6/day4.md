## 분할 정복 (Divide and Conquer)

- **Divide** → 큰 문제를 작은 문제로 분할  
  - 기저 사례(base case)를 잘 설정하여 일정 기준 이상 분할되지 않도록 해야 함
- **Conquer** → 작은 문제의 답을 모아, 큰 문제의 답을 구함

- 이전에 배운 합병 정렬이 분할 정복의 대표적인 예  
- 분할 정복은 재귀로 구현하는 것이 일반적

![image](https://github.com/user-attachments/assets/44536094-3a41-44d7-8d5d-1fe7f7e0661a)

![image](https://github.com/user-attachments/assets/dc9a9767-37fe-447b-b723-ea3e3a23d733)

![image](https://github.com/user-attachments/assets/d75e840e-b6ca-4152-a57f-c0a9986739f0)

![image](https://github.com/user-attachments/assets/3eacf7cb-2ec0-4628-90b0-d23cff153708)

## ✅ 백트래킹 (Backtracking)

> **불필요한 경로를 가지치기로 제거하여 효율적으로 답을 찾는 탐색 알고리즘**

### 🌿 핵심 개념

- **답이 될 수 없는 경우**는 탐색 대상에서 제외하여 효율적으로 답을 구함
  - 가지치기(pruning)를 통해 **연산량을 유의미하게 줄여줌**

- 가지치기를 사용하려면:
  - **현재 상태에서 도달 가능한 모든 상태가 답이 될 수 없음을** 증명해야 함

- 정확한 **시간 복잡도 계산이 어려움**

### 🧠 예시
- N-Queen 문제
- 미로 탈출
- 순열, 조합 생성 문제 등

### 🖼️ 시각적 비유
- 이미지: 실제 나무 가지를 자르는 모습  
  → "답이 될 수 없는 경로를 미리 잘라냄"을 상징


### ✅ 분할 정복 vs 백트래킹 차이점

| 구분       | 분할 정복 (Divide and Conquer)                     | 백트래킹 (Backtracking)                                   |
|------------|----------------------------------------------------|------------------------------------------------------------|
| **공통점** | - 주로 재귀적인 방식으로 문제 해결                 | - 주로 재귀적인 방식으로 문제 해결                         |
| **해결 방식** | - 문제를 하위 문제로 나누어 해결한 후 결과를 결합 | - 가능한 모든 선택을 시도하고, 실패 시 이전 단계로 되돌아감 |
| **핵심 개념** | - 하위 문제 해결 → 결과 결합 → 전체 문제 해결      | - 시도 → 불가능 시 → 되돌아가기(Backtrack)                |
| **예시**   | 병합 정렬, 퀵 정렬, 이진 탐색 등                   | 미로 찾기, N-Queen, 순열 생성 등                          |


### 💡 예시 코드 (병합 정렬 Merge Sort)
```
n, m = map(int, input().split())
s = []

def dfs():
    if len(s) == m:
        print(' '.join(map(str, s)))
        return
    for i in range(1, n + 1):
        if i not in s:
            s.append(i)
            dfs()
            s.pop()

dfs()
```
![image](https://github.com/user-attachments/assets/6e2efc23-ef42-4082-97c3-f774456425cf)

## ✅ 동적 계획법 (DP, Dynamic Programming)

### 📘 개념
- **이전에 계산한 값을 재사용**하여, 하나의 문제를 한 번만 풀게 하는 알고리즘 패러다임
- Divide & Conquer(분할 정복)와 유사하지만, **중간 결과를 저장하여 효율성**을 높이는 점에서 차이가 있음

### 🔁 핵심 아이디어
- **중복 계산 방지 = 저장된 결과 재활용**
- 이전에 계산한 값을 **메모리(배열 등)에 저장**하여 반복 작업을 줄이는 것이 핵심
  - 하위 문제의 결과를 먼저 저장하고, 이를 나중에 필요할 때 사용

### 💡 주요 기법
- **Tabulation (Bottom-Up)**: 작은 문제부터 차근차근 올라오며 해결
- **Memoization (Top-Down)**: 큰 문제에서 시작해 필요한 하위 문제의 결과를 재귀적으로 구해가며 저장

## ✅ 동적 계획법(DP)의 두 가지 접근 방식

### 🔼 Top-Down DP (재귀 + 메모이제이션)

- **큰 문제부터 시작하여** 작은 하위 문제를 재귀적으로 해결
- 이미 계산한 하위 문제 결과는 **메모이제이션(Memoization)** 기법을 통해 저장 후 재사용
- 주로 **재귀**를 활용
- 장점: 구현이 직관적  
- 단점: 함수 호출 스택 사용으로 인해 메모리 부담

#### 💡 예시 코드 (Python)
```cpp
int fibo(int n) {
    if (n <= 2) return 1; // base case
    int& ret = dp[n];     // 메모이제이션 배열 참조
    if (ret != -1) return ret;
    return ret = fibo(n - 1) + fibo(n - 2);
}
```
![image](https://github.com/user-attachments/assets/bdfb4fc3-5762-4e77-b094-09f61139cb2f)


### 🔽 Bottom-Up DP (반복문 + 테이블)
- 작은 문제부터 차근차근 해결, 큰 문제로 확장
- 주로 반복문과 배열(Table) 을 이용해 점화식 기반으로 구현
- 탑다운보다 메모리 사용이 예측 가능하고 호출 스택 부담 없음
- 기저 조건(base case) 을 명확히 정의해야 함

```
for (int i = 2; i <= 40; ++i) {
    dp[i] = dp[i - 1] + dp[i - 2];
}
```

![image](https://github.com/user-attachments/assets/708867b7-821f-4f6e-8f01-80bbae1f1054)

### ✅ Top-Down vs Bottom-Up 비교표 (마크다운 형식)

| 항목           | Top-Down 방식 (Memoization)                             | Bottom-Up 방식 (Tabulation)                                |
|----------------|----------------------------------------------------------|-------------------------------------------------------------|
| 구조           | 재귀 호출 + 메모이제이션                                | 반복문 + 테이블(Tabulation)                                |
| 접근 순서     | 큰 문제 → 작은 문제 (문제를 점점 쪼갬)                  | 작은 문제 → 큰 문제 (순차적으로 해결)                     |
| 구현 방식     | 재귀 함수 사용                                           | 반복문 사용                                                |
| 저장 방식     | 메모이제이션: 필요한 시점에 값 저장 (캐시)              | 테이블: 미리 준비된 배열에 채우는 방식                    |
| 필요 조건     | 기저 조건(Base Case) 명시 필요                         | 점화식과 Base Case 필요                                    |
| 호출 오버헤드 | 있음 (함수 호출 많음)                                   | 없음 (반복문 기반)                                         |
| 장점           | 코드 간결, 직관적 구현 가능                             | 모든 단계의 값이 명확하게 계산되어 안정적                 |
| 단점           | 스택 오버플로우 가능성 있음                             | 점화식 설계 실패 시 구조 설계가 어려움                     |
| 구입 난이도   | 상대적으로 간단 (초보자에 친숙)                         | 구조 이해와 점화식 수립이 더 어려울 수 있음               |

### ⚠️ 스택 오버플로우(Stack Overflow)

- **정의**: 너무 많은 함수 호출로 인해 **호출 스택이 가득 차서 발생하는 오류**
- 재귀 함수 호출이 깊어질 경우, 스택 메모리 한계를 초과하면서 발생
- 파이썬에서는 이 오류가 발생하면 `RecursionError`가 발생함

### 예시 (Python)
```python
def infinite_recursion():
    return infinite_recursion()

infinite_recursion()  # RecursionError: maximum recursion depth exceeded

## ✅ 동적 계획법(DP)을 사용할 수 있는 조건

동적 계획법을 적용하기 위해서는 다음 두 가지 조건을 **모두** 만족해야 함:

### 1. 겹치는 부분 문제 (Overlapping Subproblem)
- 동일한 하위 문제가 여러 번 반복적으로 등장함
- 하위 문제의 결과를 재사용할 수 있음

### 2. 최적 부분 구조 (Optimal Substructure)
- 전체 문제의 해답이 **하위 문제의 해답을 결합**하여 구할 수 있음

---

### 💡 예시: 피보나치 수열

- 문제: `N번째 피보나치 수`를 구하는 문제
- 하위 문제: `N-1번째`, `N-2번째` 피보나치 수
- 동일한 하위 문제가 반복 → 겹치는 부분 문제 조건 만족
- `F(N) = F(N-1) + F(N-2)` → 하위 문제의 답을 조합하여 전체 문제 해결 가능 → 최적 부분 구조 조건 만족

결론: **DP로 해결 가능**

※ float('inf') : 양의 무한대

## 누적합

![image](https://github.com/user-attachments/assets/e0317d55-9e62-469f-8e23-0ec1e27f2061)

![image](https://github.com/user-attachments/assets/a515c92e-ea94-458d-8306-fad967b5f0aa)

![image](https://github.com/user-attachments/assets/b28d8974-9386-4858-9ed9-eec6a7387535)

![image](https://github.com/user-attachments/assets/f3b7f3ee-3559-4813-bbb6-72d32f1b7746)

![image](https://github.com/user-attachments/assets/20c89ed0-acf1-4fbc-8ac3-ead309408e5d)
※누적합 base는 1

# DFS와 BFS

## ✅ 깊이 우선 탐색 (DFS, Depth First Search)

### 📘 정의
- 그래프 또는 트리에서 **한 가지 경로를 끝까지 탐색**한 뒤,
  더 이상 진행할 수 없을 때 **이전 경로로 되돌아가며 다른 경로 탐색**을 이어가는 방식

### 🔍 동작 방식
- 시작 노드에서 **갈 수 있는 경로가 있으면 계속 탐색**
- 더 이상 갈 수 없을 경우, **가장 가까운 갈림길(스택 기준)**로 되돌아가서 다른 경로 탐색
- 재귀 호출 또는 스택을 활용하여 구현 가능

### 🧭 비유
- **미로 탐색**: 한 방향으로 끝까지 가다가 막히면, 되돌아가서 다른 갈림길을 탐색하는 방식

### 🛠️ 사용 예시
- **모든 정점을 방문해야 하는 경우**
- **경로 탐색**, **조합 생성**, **백트래킹 기반 문제**, **싸이클 탐지** 등

## ✅ DFS의 특징 (Depth First Search)

### 🔁 구현 방식
- 일반적으로 **재귀 함수**를 사용하여 구현
- 또는 **스택(Stack)**을 이용한 반복문 방식으로도 구현 가능

### 🔍 탐색 특성
- **모든 경우의 수**에 대해 탐색을 수행 (완전 탐색)
- **사이클이 있는 그래프**에서는 **무한 루프**에 빠지지 않도록 반드시 방문 체크 필요
  - 사이클(Cycle): 한 노드에서 시작해 여러 간선을 거쳐 다시 해당 노드로 도착하는 경로

### 🚀 장점
- **BFS보다 깊은 경로**(큐)를 빠르게 찾는 데 유리함
  - 특히, 해답이 깊은 곳에 있는 경우 유리

![image](https://github.com/user-attachments/assets/ea63241a-8d4e-4cc9-889d-d10eb11d1414)

![image](https://github.com/user-attachments/assets/202621f7-3ab1-43d1-afe8-10e994f9be5a)



