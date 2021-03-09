### 벨만-포드 알고리즘(Bellman-Ford)이란?

다익스트라 알고리즘과 동일하게 그래프에서 시작 정점으로부터 다른 모든 정점까지의 최단 경로를 찾는 알고리즘 → 최단 경로(Shortest Path) 탐색 알고리즘

- *알고리즘을 개발한 두 학자의 성을 따로 붙인 이름*

**특징** 

1.  **간선의 값이 음수**일 때도 사용 가능한 알고리즘
    - 음의 간선이 존재하는 경우 다익스트라 알고리즘은 음의 간선을 피해 최단 경로를 제대로 구하지 못한다.
2. **한 정점(시작점)에서 한 정점(도착점)으로** 가는 최단경로 문제를 해결하는 알고리즘

### 음의 사이클

![Bellman](./Algorithm/bellman1.png)


1. s → a→ b →g 의 경우 
    - 일반적인 경로 → 문제 발생하지 않는다
2. s → c → d → g의 경우
    - 6+(-3) = +3 이므로 순환할 이유가 없음 → 문제 발생하지 않는다
3.  s → e → f → e → f → g 의 경우
    - 순환을 하는 경우 3+(-6) = -3만큼 줄어들기 때문에 무한 순환으로 반복 → 문제 발생한다

⇒ 최단 경로는 출발점으로부터 도달가능하며 **음의 값을 가지는 순환이 없는 경우**

: 순환을 피하기 위해서 거리 값을 갱신하는 과정을 **최대 V -1**로 제한하면 순환을 피할 수 있음

Ex) 3개의 노드인 경우 최대 2개의 간선까지만 허용 → 순환 못함

### Relaxtion

![Bellman](./Algorithm/bellman2.png) ![Bellman](./Algorithm/bellman3.png)

최단 경로문제에서 s → t →y → x → z경로나 s → t →x , s → y → z 의 경로의 결과는 동일함

결국 여러가지 **경로를 찾아보면서 현재 경로 값보다 더 적은 경로가 존재한다면 값을 변경**

### 시간복잡도

→ V - 1번 인접한 모든 간선들을 검사하는 과정을 거치기 때문에 **O(VE)**가 된다.

- O(E logV)를 가지는 다익스트라 알고리즘보다 복잡도는 높지만 음수 간선이 존재할 때 사용할 수 있는 장점, 음수 사이클 여부 판별 가능

### 벨만-포드 알고리즘 구현 특징

- 철저하게 이중 for문을 통해 가능한 모든 경우를 다 체크하는 방법
    - 시간복잡도가 큼(비효율적)
- 간선의 갯수는 많아야 V-1개
- 최단 경로는 순환을 포함하면 안 된다 → 중간에 포함하는 음수 순환이 문제를 발생

    → 무한대만큼 순환을 하는 경우가 발생

### 알고리즘

1. 시작 정점 결정 = 0
2. 모든 거리 값을 무한대로 초기화
3. 첫 번째 정점부터 인접 정점들을 탐색하며 거리를 갱신
4. 앞의 과정을 반복
5. 모두 마친 후에 한번 더 반복을 시켜주고 이때 값이 갱신되면(업데이트되면) 음의 사이클이 있다는 것을 확인

### 예시 문제 - 백준 11657(타임머신)

도시간의 버스 정보를 가지고 1번 도시에서 출발해서 나머지 도시로 가는 가장 빠른 시간을 구하는 프로그램으로 음의 간선이 존재하고 음의 사이클 또한 존재, 이 문제에서는 음의 사이클이 존재하면 -1을 출력

### 코드

```cpp
#include <iostream>
#include <vector>

using namespace std;

#define INF 987654321

int dist[502];
vector<pair<int,int>> v[502];

int main(){
    ios_base :: sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);

    int N,M;
    cin >> N >> M;

    bool cycle = false;

    for(int i = 0; i < M; i++) { //vector에 넣기
        int n1, n2, w;
        cin >> n1 >> n2 >> w;
        v[n1].push_back(make_pair(n2,w));
    }
    
    for(int i = 1; i <= N; i++) { //무한대로 초기화
        dist[i] = INF;
    }

    dist[1] = 0;
    for(int i = 1; i <= N; i++) { // N-1까지이고 N이 되면 음수 사이클이라는 소리
        for(int j = 1; j <= N; j++) {
            for(auto &n : v[j]) {
                if(dist[j] != INF && dist[n.first] > n.second + dist[j]) {
                    dist[n.first] = n.second + dist[j];
                    if(i == N)
                        cycle = true;
                }
            }
        }
    }
    if(cycle)
        cout << "-1\n";
    else {
        for(int i = 2; i <= N; i++) {
            if(dist[i] == INF)
                cout << "-1\n";
            else
                cout << dist[i] << "\n";
        }
    }
    return 0;
}
```

### 참고자료

[컴퓨터 알고리즘 기초 17강 벨만-포드 알고리즘 | T아카데미](https://youtu.be/PIT-aYPPPIQ)

[벨만-포드 알고리즘](https://ratsgo.github.io/data%20structure&algorithm/2017/11/27/bellmanford/)