# Interview-QA

This is a basic list of few questions &amp; there answers. I'll list down actual question which comes in actual interview situations.
There will be different categories of questions. I'll try to cover as much as possible. (DS & Algo, Javascript, Typescript, React, Vue, Node, Express, Next.JS, etc.)

- [**DSA**](#dsa)
- [**Javascript Questions**](#javascript-questions)

## DSA

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

---

## Javascript Questions

#### 1. Lets say you have 5 promises and you want to get the promise with exactly 2 promises results. How will you do that? Besically, you need to write a function which can accept array of promises like `Promise.all` and how many exact result you want, then function will return a promise as soon as 2 of the promises got resolved, maybe some promises can reject also, ignore those.

```js
const promises = [
  delayPromise(100, "Promise 1"),
  delayPromise(200, "Promise 2"),
  delayPromise(0, "Promise 3"),
  delayPromise(300, "Promise 4"),
  delayPromise(150, "Promise 5"),
];

function delayPromise(ms, data) {
  return new Promise((resolve) => setTimeout(() => resolve(data), ms));
}
// Write this promiseSome function
promiseSome(promises, 2)
  .then((result) => {
    console.log(result); // Output: ['Promise 3', 'Promise 1']
  })
  .catch((error) => {
    console.error(error); // Most of the time, it will not go to catch block
  });
```

<details><summary><b>Answer</b></summary>
<p>

##### This function is similar to `Promise.all` but it will resolve as soon as 2 promises got resolved.

```js
function promiseSome(promises, count) {
  return new Promise((resolve, reject) => {
    if (!Array.isArray(promises) || !Number.isInteger(count) || count <= 0) {
      reject(new Error("Invalid input"));
      return;
    }

    const results = [];
    let fulfilledCount = 0;

    function checkCompletion() {
      if (fulfilledCount === count) {
        resolve(results);
      }
    }

    promises.forEach((promise, index) => {
      promise
        .then((data) => {
          results[index] = data;
          fulfilledCount++;

          // Check if we have filled the results array with non-null values
          if (results.filter((item) => item !== null).length === count) {
            checkCompletion();
          }
        })
        .catch((error) => {
          // Fill with null if promise is rejected
          results[index] = null;
          fulfilledCount++;

          // Check if we have filled the results array with non-null values
          if (results.filter((item) => item !== null).length === count) {
            checkCompletion();
          }
        });
    });
  });
}
```

</p>

</details>

---

#### 2. There is an array of objects, you need to sort the array based on the object property. For example, if the array is

```js
const inputArray = [
  { name: "susanta", age: 27 },
  { name: "ayan", age: 28 },
  { name: "avik", age: 26 },
  { name: "souvik", age: 25 },
];
```

you need to sort the array based on the `age` property. I want to sort the array in asending order of age.

<details><summary><b>Answer</b></summary>
<p>

##### This solution is using `sort` method of array. Other approach can be sorting function using `bubble sort` or `merge sort` or `quick sort`.

```js
// Sort array based on key using JS sort method
function sortArray(arr, key) {
  return arr.sort((a, b) => a[key] - b[key]);
}

console.log(sortArray(inputArray, "age"));
```

```js
// Bubble sort approach
let bubbleSort = (inputArr, key) => {
  let len = inputArr.length;
  for (let i = 0; i < len; i++) {
    for (let j = 0; j < len; j++) {
      if (inputArr[j][key] > inputArr[j + 1]?.[key]) {
        let tmp = inputArr[j];
        inputArr[j] = inputArr[j + 1];
        inputArr[j + 1] = tmp;
      }
    }
  }
  return inputArr;
};

console.log(bubbleSort(inputArray, "age"));
```

</p>

</details>

---

#### 3. Code Snippet is provided , let me know the output.

```js
const mystery = new Array(3)
  .fill(2)
  .map((x, y) => x + y)
  .filter((x) => x % 2 === 0);

console.log(mystery);
```

<details><summary><b>Answer</b></summary>
<p>

##### Output will be `[2, 4]`, because `new Array(3).fill(2)` will create an array of length 3 with value 2. Then `map` function will add index with value, so it will be `[2, 3, 4]`. Then `filter` function will filter out odd numbers, so it will be `[2, 4]`.

</p>
</details>

---

#### 4. Remove the duplicate number from an Array in JS.

```js
const arr = [2, 2, 3, 4, 9, 6, 4, 3];
// out put should be [2,3,4,9,6]
```

<details><summary><b>Answer</b></summary>
<p>

##### Output will be `[2, 3, 4, 9, 6]`, because `new Set(arr)` will create a set of unique values, then `Array.from` will convert the set to array.

```js
const arr = [2, 2, 3, 4, 9, 6, 4, 3];
const uniqueArray = [...new Set(arr)];
console.log(uniqueArray); // [2, 3, 4, 9, 6]
```

##### Another method using `filter` function

```js
const arr = [2, 2, 3, 4, 9, 6, 4, 3];
const uniqueArray = arr.filter((element, index) => {
  return arr.indexOf(element) === index;
});
console.log(uniqueArray); // [2, 3, 4, 9, 6]
```

</p>
</details>
