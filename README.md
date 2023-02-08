# numbers-in-range
Function to check if given array of integers contains numbers in range

## Task:
Write a function that receive array of integers and performs analysis which produces following result:
1. If there are any numbers in array that can be grouped in range (for example 1,2,3,4.... ), represented as range start number + delimeter "-" + range end number
3. Any numbers that not in range represented as delimeter "," + number not in range + delimeter: ","

## Examples:
```js
compress([1, 4, 5, 2, 3, 9, 8, 11, 0]); // '0-5,8-9,11'
compress([1, 4, 3, 2]); // '1-4'
compress([1, 4]); // '1,4'
compress([1, 2]); // '1-2'
```

### Solution:
```js
function compress(list) {
  if (!Array.isArray(list)) return '';

  const sortedList = list.sort((a, b) => a - b);

  let result = '';
  let isRange = false;

  sortedList.forEach((prev, idx, array) => {
    const next = array[idx + 1];
    const afterOne = array[idx + 2];
    const diff = next - prev;

    if (diff > 1) {
      result += prev + ',';
      isRange = false;
    }

    if (diff === 1 && !isRange && afterOne - next !== 1) {
      result += prev + ',';
    }

    if (diff === 1 && !isRange && afterOne - next === 1) {
      result += prev + '-';
      isRange = true;
    }

    if (!diff) {
      result += prev;
    }
  });

  console.log(result);
  return result;
}

compress();
compress([]);
compress([1, 4, 5, 2, 3, 9, 8, 11, 0]); // '0-5,8-9,11'
compress([1, 4, 3, 2]); // '1-4'
compress([1, 4]); // '1,4'
compress([1, 2]); // '1-2'

```
