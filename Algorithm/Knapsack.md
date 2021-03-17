### Knapsack 알고리즘이란?

 Dynamic Programming 이라는 알고리즘을 배울 때 예시로 흔하게 등장하는 조합 최적화 문제의 유형, 배낭이라는 뜻을 가지고 있고 말 그대로 배낭 안에 무엇을 어떻게 최대로 넣을지 방법을 찾는 문제


**특징**

1. **DP 알고리즘**에 등장하는 단골 유형
2. **일정한 가치**와 **무게**가 정해져있을 때 **최대의 합**을 구하는 문제
3. 가끔 DP외 그리디로도 해결 가능

### 물건을 쪼갤 수 있는 Knapsack 문제

*Fractional Knapsack Problem이라고 한다*

→ 물건을 쪼갤 수 있는 문제의 경우 DP보다는 그리디로 해결 가능

- 가치가 제일 높은 애들을 최대한 담고 공간이 부족하면 하나를 쪼개서 부분적으로 넣기
- 제일 좋은 것을 가져가는 방식인 Greedy 활용

### 물건을 쪼갤 수 없는 Knapsack 문제

*0-1 Knapsack Problem이라고 한다*

→ Greedy로는 해결되지 않는 경우의 수가 존재하여 Dynamic Programming으로 해결

- DP에서는 점화식이 중요
- 점화식을 세워서 문제 해결

### 시간복잡도

→ DP의 경우 2차원 배열을 사용하는 경우에도 O(n2)이고 2차원 배열을 사용하지 않아도 물건을 넣었을 때, 넣지 않았을 때를 비교하기 때문에 이중 반복문이 들어가게 되어 O(n2)이 됨

### 알고리즘 구현 방법

- 2차원 배열 사용

⇒ 해당 물건을 넣었을 때, 넣지 않았을 때의 둘을 비교하여 가치가 더 큰 것을 가져오기

### 연습문제 - BOJ 12865(평범한 배낭)

[12865번: 평범한 배낭](https://www.acmicpc.net/problem/12865)

```cpp
#include <iostream>
#include <vector>

using namespace std;

int w[101]; // 무게
int v[101]; // 가치
int dp[101][100001];

int N, K; // 물품의 수 N, 준서가 버틸 수 있는 무게 K

int main() {

	ios::sync_with_stdio(0);
	cin.tie(0);
    
	cin >> N >> K;
	for (int i = 1; i <= N; i++) {
		cin >> w[i] >> v[i];
	}
    
	for (int i = 1; i <= N; i++) {
		for (int j = 1; j <= K; j++) {
			if (j - w[i] >= 0) { // i번째 물건을 넣을 수 있다면?
				dp[i][j] = max(dp[i-1][j], dp[i - 1][j - w[i]] + v[i]);
                // 넣지 않을 때와 넣었을 때, 둘 중 더 큰 것으로 초기화
			}
            else{ // i번째 물건을 넣을 수 없다면, 배낭 용량은 같고 넣지 않았을 때의 값으로 초기화
                dp[i][j] = dp[i-1][j];
            }
		}
	}

	cout << dp[N][K];

	return 0;
}
```