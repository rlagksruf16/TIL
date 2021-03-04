### 다익스트라(Dijkstra) 알고리즘이란?

- 다익스트라 알고리즘은 DP(다이나믹 프로그래밍)을 활용한 최단 경로(Shortest Path) 탐색 알고리즘이다

    → 현실 세계에서 인공위성 GPS 소프트웨어 등에서 많이 사용되는 알고리즘

    → 최단 거리는 여러 개의 최단 거리로 이루어져있기 떄문

- 음의 간선이 있을 경우 사용할 수 없는 알고리즘
- 우선순위 큐를 활용한다는 점을 제외하면 BFS랑 비슷한 형태

**DP인 이유?**

→ 최단경로와 같은 경우 여러개의 최단거리를 나타낼 수 있기 때문, 최단 거리를 구할 때 이전까지 구했던 최단 거리 정보를 그대로 사용

### 구현 방법: 우선순위 큐

- 최소거리 값 갱신 횟수의 증가 때문 → 속도에 이점이 있기 때문이다
    - 속도에 영향을 주는 요소는 큐에서 노드를 꺼내오는 횟수와 우선순위 큐의 갱신 횟수
    - 일반적인 큐에서 다음 요소를 꺼내오는 것보다 더 적은 값을 꺼내오는 것이 효율적
- 우선순위 큐는 힙이라는 자료구조를 이용

힙(Heap) 자료구조

- 힙 자료구조는 완전이진트리로 되어 있고, heapify 연산을 통해서 최소값 또는 최댓값으로 정렬 가능
- O(NlogN)의 시간 복잡도 소요

- 우선순위 큐를 활용한다는 점을 제외하면 BFS랑 비슷한 형태

### 시간복잡도

: V는 노드의 갯수, E는 엣지의 갯수

1. 배열 이용하는 경우
    - O(V^2)
2. 힙(우선순위 큐)를 이용하는 경우
    - O(E log V)

```cpp
#include<iostream>
#include<vector>
#include<queue>
#define INF 1e9
using namespace std;
 
int main() {
    int V,E;
    scanf("%d %d", &V ,&E); //노드의 갯수와 엣지의 갯수를 입력받습니다. 
    int start;
    scanf("%d",&start);        //시작점을 입력받습니다. 
    vector<pair<int,int> > arr[V+1];
    
    for(int i=0;i<E;i++){
        int from,to,val;
        scanf("%d %d %d", &from , &to,&val); //그래프 상의 엣지들에 대한 정보를 입력받습니다. 
        arr[from].push_back({to,val});
    }
    int dist[V+1];    //최단거리를 갱신해주는 배열입니다. 
    fill(dist,dist+V+1,INF);    //먼저 무한대로 전부 초기화를 시켜둡니다. 
    priority_queue<pair<int,int>> qu;     
    
    qu.push({0,start});    //우선순위 큐에 시작점을 넣어줍니다. 
    dist[start]=0;    //시작점의 최단거리를 갱신합니다. 
    
    while(!qu.empty()){
        int cost=-qu.top().first;    // cost는 다음 방문할 점의 dist값을 뜻합니다. 
        int here=qu.top().second;     // here을 방문할 점의 번호를 뜻합니다 
        
        qu.pop();
            
        for(int i=0; i<arr[here].size(); i++){
            int next=arr[here][i].first;
            int nextcost=arr[here][i].second;
            
            if(dist[next] > dist[here] + nextcost){    
                //현재 next에 저장된 dist의값보다 현재의 점을 거쳐서 갈 경우가 
                // 거리가 더짧으면 갱신해 주고 큐에 넣습니다. 
                dist[next]=dist[here]+nextcost;
                qu.push({-dist[next],next});
            }
        }
        
    }
    for(int i=1;i<=V;i++){
        printf("%d\n", dist[i]);
    }
```

### 1753 - 최단경로

[1753번: 최단경로](https://www.acmicpc.net/problem/1753)

```cpp
#include <string>
#include <vector>
#include <queue>
#include<iostream>
#include<cstdio>
#include<algorithm>
using namespace std;
int V, E, K, from, to, w;
vector<pair<int, int> > v[20001];
priority_queue<pair<int, int> > pq;
bool visited[20001];
int dis[20001];
int INF = 1000000;

void dijkstra() {
	dis[K] = 0;
	pq.push(make_pair(0, K));

	while (!pq.empty()) {
		int current = pq.top().second;
		int value = -pq.top().first;
		pq.pop();
		if (visited[current] == false) {
			visited[current] = true;
			for (int i = 0; i < v[current].size(); i++) {
				if (dis[v[current][i].first] > value + v[current][i].second) {
					dis[v[current][i].first] = value + v[current][i].second;
					pq.push(make_pair(-dis[v[current][i].first], v[current][i].first));
				}
			}
		}
		
	}
}
int main(void) {
	
	cin >> V;
	cin >> E;

	cin >> K; //출발점
    for (int i = 0; i < E; i++) {
		cin >> from >> to >> w;
		v[from].push_back(make_pair(to, w));
	}
	for (int i = 1; i <= V; i++) {
		dis[i] = INF;
	}
	dijkstra(); // dig 
	for (int i = 1; i <= V; i++) {
		if (dis[i] == INF) cout << "INF\n";
		else cout << dis[i] << "\n";
	}
}
```