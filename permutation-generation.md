# Permutation 


## Heap's algorithm 

https://en.wikipedia.org/wiki/Heap%27s_algorithm

```java
package com.tesco.api.price;

import java.util.Arrays;

public class Permutation {
    public static void permutation(int[] a, int k) {
        if (k == 1) {
            System.out.println(Arrays.toString(a));
        } else {
            permutation(a, k - 1);

            for (int i = 0; i < k - 1; i++) {
                if (k % 2 == 0) {
                    swap(a, i, k - 1);
                } else {
                    swap(a, 0, k - 1);
                }
                permutation(a, k - 1);
            }
        }
    }

    private static void swap(int[] array, int firstIdx, int secondIndex) {
        int tmp = array[firstIdx];
        array[firstIdx] = array[secondIndex];
        array[secondIndex] = tmp;
    }

    public static void main(String[] args) {
        permutation(new int[]{1, 2, 3}, 3);
    }
}
```


```js
const permutations = array => {
  if (array.length < 2) {
    // Base case, return single-element array wrapped in another array
    return [array];
  } else {
    let perms = [];
    for (let index = 0; index < array.length; index++) {
      // Make a fresh copy of the passed array and remove the current element from it
      let rest = array.slice();
      rest.splice(index, 1);
 
      // Call our function on that sub-array, storing the result: an array of arrays
      let ps = permutations(rest);

      // Add the current element to the beginning of each sub-array and add the new
      // permutation to the output array
      const current = [array[index]]
      for (let p of ps) {
        perms.push(current.concat(p));
      }
    };

    console.log(`Array ${array} | Perms ${perms}`);
    return perms;
  }
};


console.log(permutations([1, 2, 3]));
```

## Steinhaus–Johnson–Trotter algorithm

https://en.wikipedia.org/wiki/Steinhaus%E2%80%93Johnson%E2%80%93Trotter_algorithm

## Fisher–Yates shuffle

https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle

## Lexigographic Permutaion Algorithm

```js
const permutations = array => {
  // Sort the input
  array.sort();
  // Add a copy and initialize our list of permutations
  let perms = [array.slice()];

  while (array) {
    let [i, j, k] = Array(3).fill(array.length - 1);

    // Find the first non-increasing element
    while (i > 0 && array[i - 1] >= array[i]) i--;
    // If we don't find one, we're done!
    if (i <= 0) break;

    // Find first element larger 
    while (array[j] <= array[i - 1]) j--;

    // Swap them
    [array[i - 1], array[j]] = [array[j], array[i - 1]];

    // Reverse the suffix
    while (i < k) {
      [array[i], array[k]] = [array[k], array[i]];
      i++;
      k--;
    }
    // Add a copy of the current state of the array to the list of permutations
    perms.push(array.slice());
  }
  return perms;
};
```



*Links*
> https://www.topcoder.com/generating-permutations/
> https://medium.com/@rwillt/two-very-different-algorithms-for-generating-permutations-412e8cc0039c
> https://en.wikipedia.org/wiki/Lexicographical_order