# Bit Manipulation Problems – Java Solutions

## Overview

This repository contains solutions to fundamental bit manipulation problems. These problems focus on efficient use of bitwise operators to achieve optimal time and space complexity.

Bit manipulation is a critical topic for coding interviews, often enabling solutions that are significantly faster and more space-efficient than naive approaches.

---

## Problem Set

### 1. Single Number

#### Problem

Given a non-empty array of integers where every element appears twice except for one, find that single element.

#### Solution Strategy

Use the XOR (`^`) operation:

* XOR of a number with itself is `0`
* XOR of a number with `0` is the number itself
* XOR is associative and commutative

So, XORing all elements cancels out duplicates, leaving only the unique element.

#### Complexity

Time: O(n)
Space: O(1)

#### Implementation

```java
class Solution {
    public int singleNumber(int[] nums) {
        int element = 0;

        for (int i = 0; i < nums.length; i++) {
            element ^= nums[i];
        }

        return element;
    }
}
```

---

### 2. Counting Bits

#### Problem

Given an integer `n`, return an array `answer` where `answer[i]` is the number of `1`s in the binary representation of `i` for all `0 ≤ i ≤ n`.

#### Solution Strategy

Use dynamic programming with bit manipulation:

* Right shift (`i >> 1`) removes the last bit
* `(i & 1)` tells whether the last bit is `1`

So:

* Number of set bits in `i` = set bits in `i/2` + last bit

#### Complexity

Time: O(n)
Space: O(n)

#### Implementation

```java
class Solution {
    public int[] countBits(int n) {
        int[] answer = new int[n + 1];

        for (int i = 1; i <= n; i++) {
            answer[i] = answer[i >> 1] + (i & 1);
        }

        return answer;
    }
}
```

---

### 3. Number of 1 Bits (Hamming Weight)

#### Problem

Given an integer `n`, return the number of set bits (1s) in its binary representation.

#### Solution Strategy

* Extract the last bit using `(n & 1)`
* Right shift the number to process the next bit
* Continue until all bits are processed

#### Complexity

Time: O(log n)
Space: O(1)

#### Implementation

```java
class Solution {
    public int hammingWeight(int n) {
        int count = 0;

        while (n > 0) {
            count += (n & 1);
            n = n >> 1;
        }

        return count;
    }
}
```

---

### 4. Reverse Bits

#### Problem

Reverse bits of a given 32-bit unsigned integer.

#### Solution Strategy

* Iterate through all 32 bits
* Shift result left to make space
* Extract last bit of `n` and add it to result
* Shift `n` right

This effectively builds the reversed binary number.

#### Complexity

Time: O(1) (fixed 32 iterations)
Space: O(1)

#### Implementation

```java
class Solution {
    public int reverseBits(int n) {
        int result = 0;
        int count = 32;

        while (count > 0) {
            result = result << 1;
            result = result | (n & 1);
            n = n >> 1;
            count--;
        }

        return result;
    }
}
```

---

## Key Concepts Covered

* XOR properties
* Bit masking (`&`, `|`)
* Bit shifting (`>>`, `<<`)
* Dynamic programming with bits
* Fixed-width integer manipulation

---

## Summary

These problems demonstrate how bitwise operations can simplify logic and drastically improve efficiency. Mastery of these techniques is essential for solving low-level optimization problems and performing well in technical interviews.