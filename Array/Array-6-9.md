# Advanced Array Problems – Java Solutions

## Overview

This repository contains solutions to a set of important array-based problems, focusing on optimization techniques such as prefix/suffix computation, greedy strategies, and constant space tracking.

The implementations are designed to be efficient, avoiding unnecessary space usage and ensuring linear time complexity wherever possible.

---

## Problem Set

### 1. Product of Array Except Self

#### Problem

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all elements of `nums` except `nums[i]`. Division is not allowed.

#### Solution Strategy

The key idea is to avoid division by using prefix and suffix products:

* First pass: compute prefix product for each index
* Second pass: multiply with suffix product

This ensures that each element gets the product of all elements before and after it.

#### Complexity

Time: O(n)
Space: O(1) (excluding output array)

#### Implementation

```java
import java.util.Arrays;

class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] ans = new int[n];
        Arrays.fill(ans, 1);

        int curr = 1;
        for (int i = 0; i < n; i++) {
            ans[i] *= curr;
            curr *= nums[i];
        }

        curr = 1;
        for (int i = n - 1; i >= 0; i--) {
            ans[i] *= curr;
            curr *= nums[i];
        }

        return ans;
    }
}
```

---

### 2. Best Time to Buy and Sell Stock II

#### Problem

Given an array `prices`, where `prices[i]` is the price of a stock on day `i`, you can complete as many transactions as you like. Find the maximum profit.

#### Solution Strategy

Instead of finding global peaks and valleys explicitly:

* Capture every profitable opportunity
* Add all positive differences between consecutive days

This greedy approach ensures maximum profit accumulation.

#### Complexity

Time: O(n)
Space: O(1)

#### Implementation

```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;

        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                profit += prices[i] - prices[i - 1];
            }
        }

        return profit;
    }
}
```

---

### 3. Increasing Triplet Subsequence

#### Problem

Given an integer array `nums`, return `true` if there exists a triplet `(i, j, k)` such that `i < j < k` and `nums[i] < nums[j] < nums[k]`.

#### Solution Strategy

Track two smallest values:

* `first`: smallest element seen so far
* `second`: second smallest element

If a number greater than both is found, an increasing triplet exists.

This avoids nested loops and reduces the problem to a single pass.

#### Complexity

Time: O(n)
Space: O(1)

#### Implementation

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        int first = Integer.MAX_VALUE;
        int second = Integer.MAX_VALUE;

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] <= first) {
                first = nums[i];
            } 
            else if (nums[i] <= second) {
                second = nums[i];
            } 
            else {
                return true;
            }
        }

        return false;
    }
}
```

---

## Key Concepts Covered

* Prefix and Suffix Computation
* Greedy Algorithms
* Constant Space Optimization
* One-pass Traversal Techniques

---

## Summary

These problems emphasize optimizing both time and space complexity while maintaining clarity in implementation. They are commonly asked in coding interviews and help build strong intuition for array manipulation and greedy decision-making.
