### Greedy 알고리즘이란?

---

Greedy 알고리즘은 Greedy(욕심 많은, 탐욕적인)의 뜻을 가지고 있는 알고리즘으로 욕심쟁이, 탐욕법 알고리즘이라고도 불립니다.

Greedy 알고리즘은 경우의 수가 존재할때 경우를 선택하는 경우마다 최선이라고 생각하는 경우를 선택하는 알고리즘입니다.

즉 현재 선택해야 하는 단계에서 미래의 상황을 고려하지 않고 현재 할 수 있는 최적의 선택을 하는 알고리즘이라고 이해하시면 편할 것 같습니다.

현재 최적의 선택을 하는 알고리즘이기 때문에 항상 최적의 해를 구하지는 못합니다.

> 회의실 스케줄링, 분할 가능 배낭 문제, 거스름돈 문제 등

**특징**

1. 미래를 생각하지 않고 현재 단계에서 최적의 선택(탐욕)을 하는 알고리즘
2. 항상 최적의 해를 구할 수 없기 때문에 최적의 해를 구할 수 있는지 확인 과정이 필수

### Greedy 문제 예시(스케줄링)

---

- BOJ(백준) 1931 회의실 배정

```jsx
function solution(n,list) {
	list.sort(function(a,b) { // 회의가 끝나는 시간을 기준으로 정렬
		if(a[1] === b[1])
			return a[0]-b[0];
		else
			return a[1] - b[1];
	};
	let count = 1;
	let ends = list[0][1];
	
	for(let i = 1; i < list.length; i++) { // 회의 시작 시간과 ends 시간 비교function solution(n,list) {	list.sort(function(a,b) { // 회의가 끝나는 시간을 기준으로 정렬		if(a[1] === b[1])			return a[0]-b[0];		else			return a[1] - b[1];	};	let count = 1;	let ends = list[0][1];		for(let i = 1; i < list.length; i++) { // 회의 시작 시간과 ends 시간 비교
		if(list[i][0] >= ends) {
			count++;
			ends = list[i][1];
		}
		else
			continue;
	}
	return count;
}
```

### Greedy 문제 모음

---

[Greedy - LeetCode](https://leetcode.com/tag/greedy/)

### Ref.

---

[[이것이 코딩 테스트다] 2. 그리디 & 구현](https://freedeveloper.tistory.com/272)

[(Algorithm) 탐욕(그리디) 알고리즘(greedy algorithm) - 활동 선택 문제, 분할 가능 배낭 문제](https://www.zerocho.com/category/Algorithm/post/584ba5c9580277001862f188)