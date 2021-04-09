### Trie 알고리즘이란?

---

트라이는 사실 알고리즘이라기 보단 문자열에서의 검색을 빠르게 해주는 자료구조입니다

구성은 Tree 형태로 만들어지며 문자열에 관한 코딩 문제들에 kmp와 더불어 자주 쓰입니다

> 검색어 자동완성, 사전에서 찾기, 문자열 검사 부분에서 주로 사용됨

**특징**

1. 탐색은 빠르나(장점) 저장공간 측면에서 공간의 크기가 크다(단점)
2. 시간복잡도는 O(문자열의 길이)

### Trie 자료구조 동작 방법

---

[](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwNWfF%2FbtquI06bYM5%2Fm22bzwlkbL5Eab22O2z8zk%2Fimg.png)


- 루트 노드에는 어떠한 단어도 들어가지 않고, 루트 아래 노트부터 문자열의 접두사가 나타난다
- Tree의 형태로 나타나며 결론적으로 루트 노드 아래에는 총 26개가 존재하게 된다 → 포인터가 최대 26개

### 시간복잡도

---

문자열에서 BinarySearchTree를 이용하여 검색했을 때, 문자열의 길이가 M이면 **O(MlogN)**의 시간복잡도를 가진다

반면 트라이를 이용한다면 **O(M)**의 시간복잡도를 가지고 문자열을 검색할 수 있다.

최종 메모리: **O(M)**

### 공간복잡도

---

공간의 경우 숫자에 대한 트라이일 경우 0~9로 10개의 포인터 배열, 알파벳의 경우 a~z로 26개의 포인터 배열이 존재해야 한다.

최종 메모리: **O(포인터의 크기*포인터 배열의 갯수* 트라이에 존재하는 총 노드의 개수)**

### Trie 구현 방법

---

```jsx
struct Trie { 
	bool finish; // 끝나는 지점을 표시해줌 
	Trie* next[26]; // 26가지 알파벳에 대한 트라이 

	// 생성자 
	Trie() : finish(false) { 
		memset(next, 0, sizeof(next)); 
	}
	
	// 소멸자 
	~Trie() { 
		for (int i = 0; i < 26; i++) {
			if (next[i]) 
				delete next[i]; 
		}
	}
	
	// 트라이에 문자열 삽입 
	void insert(const char* key) { 
		if (*key == '\0') 
			finish = true; // 문자열이 끝나는 지점일 경우 표시 
		else { 
			int curr = *key - 'A'; 
			if (next[curr] == NULL) 
				next[curr] = new Trie(); // 탐색이 처음되는 지점일 경우 동적할당 
			next[curr]->insert(key + 1); // 다음 문자 삽입 
		} 
	}
	
	// 트라이에서 문자열 찾기 
	Trie* find(const char* key) { 
		if (*key == '\0') 
			return this; // 문자열이 끝나는 위치를 반환 
		int curr = *key - 'A'; 
		if (next[curr] == NULL) 
			return NULL; // 찾는 값이 존재하지 않음 
		return next[curr]->find(key + 1); // 다음 문자를 탐색 
	}
};

```

### Trie 문제 모음

---

[Trie - LeetCode](https://leetcode.com/tag/trie/)


### Ref.

--

[[자료구조] 트라이 (Trie) C++ 구현](https://eun-jeong.tistory.com/29)
[tistory 블로그](https://jason9319.tistory.com/129)