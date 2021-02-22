### Union-Find 알고리즘이란?

- Disjoint-set(상호 배타적 집합 == 서로소 )를 표현할 때 사용하는 알고리즘

    → 두 집합 사이의 교집합 X, 두 집합의 합집합이 전체집합

- Disjoint-set을 표현하기 위해서 합친다는(Union)과 찾는(Find) 연산을 모두 이용해야 하기 때문에 Union-Find 알고리즘이라고 부름 + 초기화 연산
    - 총 3개의 연산을 포함하는 알고리즘( Union + Find + 초기화 )
        - **Union**: 두 원소가 주어질 때 이들이 속한 두 집합을 하나로 합치기
        - **Find**: 어떤 원소가 주어질 때 이 원소가 속한 집합을 반환
        - **초기화**: n개의 원소가 각각의 집합에 포함되어 있도록 만들기
- 주로 **트리구조**로 표현(벡터, 배열, 연결 리스트 등으로 표현 가능)

⇒ Uion-Find 알고리즘은 노드간 연결 관계를 파악하고 특정 간선을 연결할 시 노드 연결관계가 어떻게 변화하는지 파악하는 알고리즘

Disjoint-set이란?
→ 서로 중복되지 않은 부분 집합들로 나눠진 원소들에 대한 정보를 저장하고 조작하는 자료구조
  - 전체 집합에서 구성 원소들이 겹치지 않게 분할하는데 사용
  - 서로 다른 원소들이 같은 집합에 속한지 여부 판별하는데 사용

### 배열로 구현

- 가장 단순한 방법
- Find 연산은 O(1)에 처리 가능 → 인덱스 참조
- Union 연산은 O(n)의 시간이 소요 → 원소의 갯수만큼 순회(n개)
    - 원소가 속한 집합의 모든 원소들을 같은 집합의 번호로 변경해야 함

⇒ Union 연산에서 많은 시간을 소요하여 비효율적

### **트리로 구현**

- 배열보다 더 빠른 방법을 찾기 위해 나온 방법
- Find 연산 → Best: O(1), Worst: O(n)
    - 높이가 길어질 경우 O(n) 가능
- Union 연산 → O(n)
    - 연산의 대상이 되는 노드를 찾고 그 노드의 루트를 찾아 다른 쪽의 자손으로 넣기만 하면 됨
    - 루트를 찾는 Find 연산이 전제

⇒ 최악의 경우 한쪽으로 쏠리는 사향 트리(Skewed tree) 가능

Skewed Tree(사향 트리)
→ 한쪽으로 기울어진 트리라고 하며 편향 트리라고 하기도 함
- 최악...

트리의 Skewed Tree를 막기 위한 최적화 방법 등장

### Union by Rank → Union 단계

- Union 파트에서 두 트리를 합칠 때 높이가 더 낮은 트리를 높이가 높은 트리의 자손으로 넣어주는 방식

    → 연산 순서에 따라 트리가 Skewed Tree가 될 수 있기 때문

- 높이가 같으면 높이를 기준의 높이 +1로 저장

    → 높이가 같은 두 트리를 붙이며 높이는 기존 트리 +1이 되기 때문

⇒ 해당 방식으로 진행하면 높이가 유지 or +1씩 증가하여 시간복잡도 O(logn)

### Path Compression → Find 단계

- find가 재귀로 돌아가는데 최적화가 자동으로 수행되게끔 하는 방법
- 중복되는 연산을 줄이기 위한 부모를 찾아낸 루트로 변경

    → find 연산 시 경로 따라 올라가는 것이 아니라 바로 루트를 찾을 수 있어 중복되는 연산 줄여줌

### 최적화 고려한 Union-Find Code

```cpp
// 초기화 연산
int root[MAX_SIZE];
for (int i = 0; i < MAX_SIZE; i++) {
  root[i] = i;
}

// find 연산
int find(int x) {
  if (root[x] == x) {
      return x;
  } else {
      // find 하면서 만난 모든 값의 부모 노드를 root로 -> path compression
      return root[x] = find(root[x]);
  }
}

void union(int x, int y){
   x = find(x);
   y = find(y);

   // 두 값의 root가 같으면 X
   if(x == y)
     return;

   // 낮은 걸 높은 거 밑에 -> union by rank
   if(rank[x] < rank[y]) {
     root[x] = y; // x의 root를 y로 변경
   } else {
     root[y] = x; // y의 root를 x로 변경

     if(rank[x] == rank[y])
       rank[x]++; // 만약 높이가 같다면 합친 후 x+1
   }
}
```

### BOJ - 1717 문제

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <string>

using namespace std;

int N,M,s,a,b;

vector<int> parent, nod;

int find(int z) {
    if(parent[z] == z)
        return z;

    return parent[z] = find(parent[z]);
}

void merge(int x, int y) {
    x = find(x);
    y = find(y);
    
    if(x == y)
        return;
    
    if(nod[x] < nod[y])
        parent[x] = y;
    else if(nod[x] > nod[y])
        parent[y] = x;
    else {
        parent[y] = x;
        nod[x]++;
    }
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);

    
    cin >> N >> M;
    
    for(int i = 0; i <= N; i++) {
        parent.push_back(i);
        nod.push_back(1);
    }
    for(int j = 0; j < M; j++) {
        cin >> s >> a >> b;
        
        if(s == 0) { // merge
            merge(a,b);
        }
        else {
            if(find(a) == find(b))
                cout << "YES\n";
            else
                cout << "NO\n";
        }
    }
    return 0;
}
```

### 문제들

[Union-Find](https://www.acmicpc.net/workbook/view/900)