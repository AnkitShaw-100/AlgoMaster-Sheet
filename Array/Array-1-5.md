# Algomaster DSA Sheet – Java Solutions

This repository contains my solutions to selected problems from the Algomaster DSA Sheet, implemented in Java. Each problem is solved with an emphasis on optimal approaches, in-place modifications where possible, and clear understanding of underlying patterns.

---

## 1. Move Zeroes

### Problem Statement

Given an integer array `nums`, move all `0`s to the end of the array while maintaining the relative order of the non-zero elements. The operation must be performed in-place.

### Approach

We use a two-pointer technique:

* Maintain a pointer `pointer` to track the position where the next non-zero element should be placed.
* Traverse the array:

  * If the current element is non-zero, place it at `pointer` and increment `pointer`.
* After placing all non-zero elements, fill the remaining positions with `0`.

### Time Complexity

O(n)

### Space Complexity

O(1)

### Code

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int n = nums.length;
        int pointer = 0;

        for (int i = 0; i < n; i++) {
            if (nums[i] != 0) {
                nums[pointer] = nums[i];
                pointer++;
            }
        }

        while (pointer < n) {
            nums[pointer] = 0;
            pointer++;
        }
    }
}
```

---

## 2. Remove Duplicates from Sorted Array

### Problem Statement

Given a sorted array `nums`, remove the duplicates in-place such that each element appears only once and return the new length.

### Approach

* Since the array is sorted, duplicates will be adjacent.
* Maintain a pointer `pointer` that tracks the position of the last unique element.
* Traverse the array:

  * If the current element is different from `nums[pointer]`, increment `pointer` and update the value.

### Time Complexity

O(n)

### Space Complexity

O(1)

### Code

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int n = nums.length;
        int pointer = 0;

        for (int i = 0; i < n; i++) {
            if (nums[i] != nums[pointer]) {
                pointer++;
                nums[pointer] = nums[i];
            }
        }

        return pointer + 1;
    }
}
```

---

## 3. Best Time to Buy and Sell Stock

### Problem Statement

Given an array `prices` where `prices[i]` is the price of a stock on day `i`, find the maximum profit you can achieve by buying on one day and selling on another later day.

### Approach

* Track the minimum price seen so far.
* For each day:

  * Calculate the profit if sold on that day.
  * Update maximum profit accordingly.

### Time Complexity

O(n)

### Space Complexity

O(1)

### Code

```java
class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;

        for (int i = 0; i < prices.length; i++) {
            if (prices[i] < minPrice) {
                minPrice = prices[i];
            } else {
                maxProfit = Math.max(maxProfit, prices[i] - minPrice);
            }
        }

        return maxProfit;
    }
}
```

---

## 4. Majority Element

### Problem Statement

Given an array `nums`, return the element that appears more than ⌊n/2⌋ times. It is guaranteed that such an element exists.

### Approach

* Use a HashMap to count frequency of each element.
* While iterating:

  * Update the count of the current element.
  * If its count exceeds `n/2`, return it immediately.

### Time Complexity

O(n)

### Space Complexity

O(n)

### Code

```java
import java.util.HashMap;

class Solution {
    public int majorityElement(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int n = nums.length;

        for (int i = 0; i < n; i++) {
            int num = nums[i];
            map.put(num, map.getOrDefault(num, 0) + 1);

            if (map.get(num) > n / 2) {
                return num;
            }
        }

        return -1;
    }
}
```

---

## 5. Rotate Array

### Problem Statement

Given an array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

### Approach

* Create a temporary array of the same size.
* For each element at index `i`, place it at `(i + k) % n` in the new array.
* Copy the temporary array back into the original array.

### Time Complexity

O(n)

### Space Complexity

O(n)

### Code

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        int[] temp = new int[n];

        for (int i = 0; i < n; i++) {
            temp[(i + k) % n] = nums[i];
        }

        for (int i = 0; i < n; i++) {
            nums[i] = temp[i];
        }
    }
}
```

---

## Summary

These problems focus on fundamental techniques such as:

* Two-pointer approach
* Greedy methods
* Hashing
* In-place array manipulation

They form a strong foundation for solving more complex DSA problems efficiently.
