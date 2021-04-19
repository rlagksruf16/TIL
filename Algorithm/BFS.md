### BFS 알고리즘이란?

---

BFS(Breadth-First-Search) 알고리즘은 그래프 탐색 방법 중의 1개로 인접한 노드(가까운 노드)를 먼저 탐색하는 방법이다. 두 노드 사이의 최단 경로 또는 임의의 경로를 찾고 싶을 때 선택되는 방법이다.

***그래프 탐색이란?***

→ 하나의 정점에서부터 차례대로 다른 모든 정점들을 한 번씩 방문하는 것

Ex) 특정 도시에서 다른 도시로 이동, 전자 회로에서 특정 단자가 연결되어 있는 여부 확인

**특징**

1. 깊은 탐색(DFS)가 아닌 넓게 탐색(BFS) 하는 방법이다.
2. 최단 경로를 찾고 싶을 때 활용하는 알고리즘
3. 큐(queue)를 사용하는 알고리즘

### BFS 과정

[https://gmlwjd9405.github.io/images/algorithm-dfs-vs-bfs/bfs-example.png](https://gmlwjd9405.github.io/images/algorithm-dfs-vs-bfs/bfs-example.png)

### BFS 구현 방법

---

BFS는 코드 언어에 상관없이 Queue(큐)를 이용하여 해결

- 방문 여부 확인 배열, queue 배열 필요
- 탐색 시작 후 방문하지 않았다면 방문 체크 후 탐색 진행

```cpp
const graph = {
  A: ["B", "C"],
  B: ["A", "D"],
  C: ["A", "G", "H", "I"],
  D: ["B", "E", "F"],
  E: ["D"],
  F: ["D"],
  G: ["C"],
  H: ["C"],
  I: ["C", "J"],
  J: ["I"]
};

const bfs = (graph, start) => {
	visit = []; // 탐색 확인 여부 검사
	queue = []; // 탐색해야할 노드

	visit.push([start[0], start[1]]);
	queue.push(start); // 탐색 시작

	while(queue.length !== 0) {
		const node = queue.shift();
		if(!visit.includes(node)) {
			visit.push(node);
			queue = [ ...needVisit, ...graph[node]];
		}
	}
	return visit;
};
				
```

### BFS 문제 모음

---

[Breadth-first Search - LeetCode](https://leetcode.com/tag/breadth-first-search/)

Ref

---

[[알고리즘] 너비 우선 탐색(BFS)이란 - Heee's Development Blog](https://gmlwjd9405.github.io/2018/08/15/algorithm-bfs.html)