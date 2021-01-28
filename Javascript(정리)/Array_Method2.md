# 자바스크립트 배열 Method Part 2


## slice()

- 배열에서 선택한 인덱스의 요소들을 잘라 새로운 배열을 만드는 메서드
- 괄호 안에 시작 인덱스는 포함하고 마지막 인덱스의 해당 값은 포함하지 않는다

```jsx
let vehicle = ["car", "bike", "plane", "truck"];
let arr = vehicle.slice(1,3);
console.log(arr); // ["bike", "plane"]
```

## filter()

- `filter()` 메서드는 특정 조건에 따라 배열을 필터링 하는 메서드
- 새로운 배열을 생성한다

```jsx
let nums = [1,5,34,2,3];

function isCheck(value) {
	return value < 10;
}
let arr = nums.filter(isCheck);
console.log(arr); // [1,5,2,3]
```

## find()

- 특정 조건에 해당하는 가장 첫 번째 원소를 찾아 리턴하는 메서드

```jsx
let nums = [1,5,34,2,3];
function isCheck(value) {
	return value > 10;
}
let arr = nums.find(isCheck);
console.log(arr); // 34
```

## map()

- 기본 배열에서 각 원소에 특정 함수를 불러 적용한 후 새로운 배열을 리턴하는 메서드

```jsx
let nums = [9, 16, 25, 36];
let arr = nums.map(Math.sqrt);
console.log(arr); // [3, 4, 5, 6]
```

## some()

- 배열의 원소들 중 조건에 해당하는 것이 하나라도 있는지 여부를 판별하는 메서드
- 원소들 중 하나도 조건에 부합하지 않으면 false 리턴, 있으면 true 리턴

```jsx
let nums = [1,5,34,2,3];
function isCheck(value) {
	return value > 10;
}
let tf = nums.some(isCheck); 
console.log(tf) // true
```

## every()

- 배열의 모든 원소들이 해당 조건에 부합하는지 여부를 판별하는 메서드
- 모두 부합하면 true, 아니면 false 리턴

```jsx
let nums = [1,5,34,2,3];
function isCheck(value) {
	return value >= 1;
}
let tf = nums.every(isCheck);
console.log(tf) // true
```

## findIndex()

- 배열의 원소들 중 조건에 해당하는 가장 첫 번째 원소의 index를 리턴하는 메서드
- `findIndex()` 에는 함수만 들어가야 한다

```jsx
let nums = [1,2,3,4,5];
let temp = nums.findIndex(e => e % 2 == 1);
console.log(temp); // 0
```

## include()

- 배열의 원소들 중 조건에 해당하면 true, 아니면 false를 리턴하는 메서드

```jsx
let nums = [1,2,3,4,5];
let temp = nums.include(1);
console.log(temp); // true
```

## indexOf()

- 배열의 원소들 중 해당하는 원소가 있으면 그 원소의 index 값을 리턴하는 메서드
- 배열에 없는 경우 `-1` 을 리턴

```jsx
let nums = [1,2,3,4,5];
let temp = nums.indexOf(1);
console.log(temp); // 0
let tmp = nums.indexOf(10);
console.log(tmp); // -1
```

## isArray()

- 해당 object가 배열인지 아닌지 여부를 리턴하는 메서드

```jsx
let nums = [1,2,3,4,5];
conosole.log(nums.isArray()); // true
```