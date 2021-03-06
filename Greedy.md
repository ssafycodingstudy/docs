## 탐욕법(그리디) 알고리즘

탐욕적이라는 말은 '현재 상황에서 지금 당장 좋은 것만 고르는 방법'을 의미한다. 그리디 알고리즘을 이용하면 매 순간 가장 좋아 보이는 것을 선택하며, 현재의 선택이 나중에 미칠 영향에 대해서는 고려하지 않는다.

그리디 알고리즘의 문제 유형은 **'사전에 외우고 있지 않아도 풀 수 있을 가능성이 높은 문제 유형'**이라는 특징이 있다. 그리디 알고리즘 유형의 문제는 매우 다양하기 때문에 암기한다고 해서 항상 잘 풀 수 있는 알고리즘 유형이 아니다. 사전 지식 없이 풀 수 있는 문제도 있겠지만, 많은 유형을 접해보고 문제를 풀어보며 훈련을 해야 한다.

**코딩 테스트에서 출제되는 그리디 알고리즘** 유형의 문제는 **문제를 풀기 위한 최소한의 아이디어를 떠올릴 수 있는 능력을 요구**한다. 즉, 특정 문제를 만났을 때 단순히 현재  상황에서 가장 좋아보이는 것만 선택해도 문제를 풀 수 있는지 파악할 수 있어야 한다.

그리디 알고리즘은 기준(현재 상황)에 따라 좋은 것을 선택하는 일고리즘이므로 문제에서 '가장 큰 순서대로', '가장 작은 순서대로'와 같은 기준을 알게 모르게 제시해준다. 대체로 이 기준은 정렬 알고리즘을 사용했을 때 만족시킬 수 있으므로 그리디 알고리즘 문제는 자주 정렬 알고리즘과 짝을 이뤄서 출제된다.



![image](https://user-images.githubusercontent.com/50684682/130548777-5b4f0855-4bb5-456a-a312-29c430875bfe.jpg)



대표적인 그리디 문제, 거스름돈 (https://www.acmicpc.net/problem/5585)

물건 가격이 n이라면, 받아야하는 거스름돈은 1000 - n이고,  이를 잔돈 중 크기가 큰 단위의 잔돈으로 나누면서 잔돈의 갯수를 구한다. 문제를 푸는데 필요한 아이디어는 **'가장 큰 화폐 단위부터' 돈을 거슬러 주는 것**이다.

그러나 이것이 과연 최적의 해인지 확인하는 과정이 필요하다. 예를 들어서 800원을 거슬러줘야 하는데, 화폐 단위가 500원, 400원, 100원인 경우라면 위의 문제를 푼 알고리즘으로는 500원, 100원, 100원, 100원으로 4개의 동전을 거슬러줘야 한다고 나오지만, 실제로 필요한 최소 동전의 갯수는 2개이다.

거스름돈 문제를 그리디 알고리즘으로 해결할 수 있던 이유는 1, 5, 10, 50, 100, 500의 잔돈이 배수 관계이기 때문에 작은 단위의 동전을 조합해도 다른 해가 나올 수 없기 때문이다. 대부분의 그리디 알고리즘 문제에서는 이와 같이 **문제 풀이를 위한 아이디어를 떠올리고, 이것이 실제로 최적해를 도출할 수 있는지 검토하는 과정**이 필요하다.



## 그리디 알고리즘 연습을 위한 문제

행렬 (https://www.acmicpc.net/problem/1080)

신입 사원 (https://www.acmicpc.net/problem/1946)

크게 만들기 (https://www.acmicpc.net/problem/2812)

센서 (https://www.acmicpc.net/problem/2212)

