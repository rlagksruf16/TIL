### 정의

- 최소 비용 신장 트리 알고리즘이라고 불림
- MST를 구현하기 위해 사용하는 알고리즘
- 탐욕적인 방법(그리디)를 이용하여 네트워크(가중치를 간선에 할당한 그래프)의 모든 정점을 최소 비용으로 연결하는 최적 해답을 구하는 것

⇒ 정점들을 가장 적은 비용으로 연결

### 문제 예시

  Ex) 도로 건설(도시들을 연결하면서 도로의 길이 최소), 전기회로(단자 모두 연결하면서 전선의 길이 최소) 등등 

그래프에 정점(vertex)와 간선(edge)가 있는데, 간선에는 가중치가 포함

  → 그래프 내의 모든 정점을 포함하고 사이클이 없는 연결 선을 그렸을 때, 가중치의 합이 최소인 것을 구하기

- 신장의 트리는 정점의 갯수가 n개일 때, 간선이 n-1개

### Kruskal 알고리즘 구현

- **Greedy 활용 + 사이클 형성 X**
- 닥치는대로 Greedy하게 간선을 포함시키면 무조건 사이클 형성이 되므로 간선이 포함되었는지 안 포함되었는지를 확인하는 **Union-Find 방법 활용**

Union-find 개념 설명  

```java
public static void union(int x, int y) { // 네트워크 형성
        x = find(x);
        y = find(y);
        if(x != y)
            parent[y] = x;
    }
	
    public static int find(int x) { // 네트워크 같은지 비교
        if(parent[x] == x) {
            return x;
        }
        return parent[x] = find(parent[x]);
    }
    public static boolean isSameParent(int x, int y) {
        x = find(x);
        y = find(y);
        if(x == y) return true;
        else return false;
    }
```