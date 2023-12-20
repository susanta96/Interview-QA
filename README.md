# Interview-QA

This is a basic list of few questions &amp; there answers. I'll list down actual question which comes in actual interview situations.
There will be different categories of questions. I'll try to cover as much as possible. (DS & Algo, Javascript, Typescript, React, Vue, Node, Express, Next.JS, etc.)

- [**DS & Algo**](#dsa)

## Actual Interview Questions

#### 1. There is a Number input, you need to reverse the number without converting it to string. For example, if the input is `1234`, the output should be `4321`.

```js
const input = 1234;
const output = reverse(input);
console.log(output); // 4321
```

<details><summary><b>Answer</b></summary>
<p>

##### This is a short function using loop

```js
function reverse(num) {
  let rev = 0;
  while (num > 0) {
    rev = rev * 10 + (num % 10);
    num = Math.floor(num / 10);
  }
  return rev;
}

const input = 1234;
const output = reverse(input);
console.log(output); // 4321
```

</p>

</details>

---

#### 2. Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

```js
const nums = [1, 0, -1, 2, -2, 3, 5, 6];
const target = 4;
const output = twoSum(nums, target);
console.log(output); // [[1, 3], [-1, 5], [-2, 6]]
```

<details open><summary><b>Answer</b></summary>
<p>

##### This is nested loop solution, which leads to O(n^2) time complexity

```js
function twoSum(nums, target) {
  const result = [];
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        result.push([nums[i], nums[j]]);
      }
    }
  }
  return result;
}
```

This is optimized solution using Map, which leads to O(n) time complexity

```js
function findPairs(arr, target) {
  let pairs = [];
  let comp = new Map();
  for (let i = 0; i < arr.length; i++) {
    if (comp.has(arr[i])) {
      pairs.push([comp.get(arr[i]), arr[i]]);
    }
    comp.set(target - arr[i], arr[i]);
  }
  return pairs;
}

const arr = [1, 0, -1, 2, -2, 3, 5, 6];
const target = 4;
console.log(findPairs(arr, target)); // [[1, 3], [-1, 5], [-2, 6]]
```

</p>

</details>
