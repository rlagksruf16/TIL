# 자바스크립트 배열 Method Part 1

## Pop()

- 배열에서 마지막 요소를 삭제하는 메서드
- `pop()` 는 삭제한 요소를 return 한다.

```jsx
let vehicle = ["car", "bike", "plane"];
vehicle.pop(); // "plane"
console.log(vehicle); // ["car", "bike"]
```

## Push()

- 배열에서 새로운 요소를 맨 뒤에 추가하는 메서드

```jsx
let vehicle = ["car", "bike", "plane"];
vehicle.push("truck");
console.log(vehicle); // ["car", "bike", "plane", "truck"]
```

## toString()

- 배열을 String으로 변경하는 메서드

```jsx
let vehicle = ["car", "bike", "plane"];
let tmp = vehicle.toString();
console.log(tmp); // "car,bike,plane"
```

## join()

- 해당 배열을 String으로 join해주는 메서드
- `toString()`이랑 다른 점은 join 안의 값으로 배열 요소들을 연결시켜준다

```jsx
let vehicle = ["car", "bike", "plane"];
let tmp = vehicle.join("-");
console.log(tmp); // "car-bike-plane"
```

## splice()

- 배열에서 특정 아이템을 추가하고 삭제하는 메서드
- `array.splice(index, many, element(1) ... element(n) );`
    - index = 배열 내에서 추가되어야 할 인덱스 위치
    - many = index 위치부터 삭제될 갯수, 만약 many 가 0이면 삭제 안됨
    - element(1) ~ element(n) = 추가될 항목들

    ```jsx
    let vehicle = ["car", "bike", "plane"];
    vehicle.splice(1,0,"1","2");
    console.log(vehicle); // ["car", "1", "2", "bike", "plane"];
    ```

## sort()

- 알파벳 순 또는 숫자 순으로 정렬 해주는 메서드
- 정렬 후 해당 배열에 결과값 return

```jsx
let nums = [1,5,34,2,3];
nums.sort();
console.log(nums); // [1,2,3,5,34];
```

## shift()

- 배열의 맨 앞 요소를 삭제하는 메서드

```jsx
let vehicle = ["car", "bike", "plane"];
vehicle.shift();
console.log(vehicle); // ["bike", "plane"];
```

## unshift()

- 배열의 맨 앞 부분에 특정 요소를 추가하는 메서드

```jsx
let vehicle = ["car", "bike", "plane"];
vehicle.unshift("truck");
console.log(vehicle); // ["truck", "car", "bike", "plane"];
```

## reverse()

- 배열의 순서를 뒤집는 메서드

```jsx
let vehicle = ["car", "bike", "plane"];
vehicle.reverse();
console.log(vehicle); // ["plane", "bike", "car"];
```

## concat()

- 두 개 이상의 배열을 합쳐서 하나로 만드는 메서드
- 먼저 온 배열이 앞에 정렬되고 뒤의 배열이 뒤에 정렬된다

```jsx
let vehicle = ["car", "bike", "plane"];
let nums = [1, 5, 34, 2, 3];
let results = vehicle.concat(nums);
console.log(results) // ["car", "bike", "plane", 1, 5, 34, 2, 3];
```