
# Greedy Algorithm(그리디 알고리즘)

- Greedy는 말 그대로 "탐욕스러운" 이란 뜻이다.

- Greedy Algorithm은 선택의 순간마다 당장 눈 앞에 보이는 최적의 상황만을 쫓아 최종적인 해답에 도달하는 알고리즘이다.
순간마다 하는 선택은 그 순간에서 만큼은 최적이지만, 누적된 선택들에 대해선 최적이라는 보장이 없다.

- Greedy Algorithm은 "최적해"를 구할 때 사용되는 근사적인 방접이다.

<br>

# Greedy Algorithm 문제를 해결하는 방법

1. 선택 절차(Selection Procedure) : 현재 상태에서의 최적의 해답을 선택한다.

2. 적절성 검사(Feasibility Check) : 선택된 해가 문제의 조건을 만족하는지 검사한다.

3. 해답 검사(Soluctino Check) : 원래의 문제가 해결되었는지 검사하고, 해결되지 않았다면 다시 선택 절차로 돌아가 과정을 반복한다.

<br>

# Greedy Algorithm의 2가지 조건

- Greedy Algorithm이 잘 작동하는 문제는 대부분 "탐욕스러운 선택 조건(greedy choice property)"과 최적 "부분 구조 조건(optimal substructure)"이라는 두 가지 조건이 만족된다.
   - "탐욕스러운 선택 조건"은 이전 선택이 이후의 선택에 영향을 주지 않는다는 것이다.
   - "최적 부분 구조 조건"은 문제에 대한 최적해가 부분문제에 대해서도 역시 최적이라는 뜻이다.

- 위의 두 가지 조건이 성립하지 않는 경우에는 탐욕 알고리즘은 최적해를 구하지 못한다.
- 하지만, 이러한 경우엥도 탐욕 알고리즘은 "근사 알고리즘"으로 사용할 수 있으며, 대부분의 경우 계산 속도가 빠르기 때문에 실용적으로 사용할 수 있다.(어느 정도 최적해를 구하기 위해선 엄밀한 증명이 필요하다)
- 특별한 구조를 가지고 있는 문제에 대해선 탐욕 알고리즘이 언제나 최적해를 찾아낼 수 있다. 이런 특별한 구조를 "매트로이드 구조"라고 한다.






