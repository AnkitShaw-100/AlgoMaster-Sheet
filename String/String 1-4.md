# String Manipulation Problems – Java Solutions

## Overview

This repository contains solutions to fundamental string manipulation problems, focusing on efficient traversal techniques, two-pointer strategies, and careful handling of edge cases such as spaces and non-alphanumeric characters.

The implementations prioritize:

* Linear time complexity
* In-place or minimal extra space usage
* Readable and maintainable code

---

## Problem Set

### 1. Is Subsequence

#### Problem

Given two strings `s` and `t`, determine if `s` is a subsequence of `t`. A subsequence is formed by deleting some (or no) characters without changing the order of the remaining characters.

#### Solution Strategy

Use a two-pointer approach:

* Pointer `i` for string `s`
* Pointer `j` for string `t`
* Traverse `t`, and whenever characters match, move pointer `i`
* If `i` reaches the end of `s`, it is a subsequence

#### Complexity

Time: O(n + m)
Space: O(1)

#### Implementation

```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        int i = 0, j = 0;

        while (i < s.length() && j < t.length()) {
            if (s.charAt(i) == t.charAt(j)) {
                i++;
            }
            j++;
        }

        return i == s.length();
    }
}
```

---

### 2. Valid Palindrome

#### Problem

Given a string `s`, determine if it is a palindrome considering only alphanumeric characters and ignoring cases.

#### Solution Strategy

Use two pointers:

* One from the start and one from the end
* Skip non-alphanumeric characters
* Compare characters in lowercase form

This ensures correct comparison while ignoring irrelevant characters.

#### Complexity

Time: O(n)
Space: O(1)

#### Implementation

```java
class Solution {
    public boolean isPalindrome(String s) {
        int start = 0;
        int last = s.length() - 1;

        while (start <= last) {
            char currFirst = s.charAt(start);
            char currLast = s.charAt(last);

            if (!Character.isLetterOrDigit(currFirst)) {
                start++;
            } 
            else if (!Character.isLetterOrDigit(currLast)) {
                last--;
            } 
            else {
                if (Character.toLowerCase(currFirst) != Character.toLowerCase(currLast)) {
                    return false;
                }
                start++;
                last--;
            }
        }

        return true;
    }
}
```

---

### 3. Reverse Words in a String

#### Problem

Given a string `s`, reverse the order of words. A word is defined as a sequence of non-space characters. The output should not contain leading or trailing spaces, and multiple spaces between words should be reduced to a single space.

#### Solution Strategy

* Trim leading and trailing spaces
* Split the string using one or more spaces as delimiter
* Traverse the array in reverse order
* Build the result using a `StringBuilder`

#### Complexity

Time: O(n)
Space: O(n)

#### Implementation

```java
class Solution {
    public String reverseWords(String s) {
        s = s.trim();
        String[] arr = s.split("\\s+");

        StringBuilder ans = new StringBuilder();

        for (int i = arr.length - 1; i >= 0; i--) {
            ans.append(arr[i]).append(" ");
        }

        return ans.toString().trim();
    }
}
```

---

### 4. Longest Common Prefix

#### Problem

Given an array of strings `strs`, find the longest common prefix shared among all the strings. If there is no common prefix, return an empty string `""`.

#### Solution Strategy

Instead of comparing all strings pairwise, we can optimize by:

* Sorting the array of strings lexicographically
* After sorting:

  * The **first** and **last** strings will be the most different
  * The common prefix of these two strings will be the common prefix of the entire array

### Steps

1. Sort the array
2. Take:

   * `s1 = first string`
   * `s2 = last string`
3. Compare characters of `s1` and `s2` one by one
4. Stop when characters differ
5. Return the substring up to that index

This works because sorting ensures that strings with similar prefixes are grouped together.

#### Complexity

Time: O(n log n)
Space: O(1)

#### Implementation

```java
import java.util.Arrays;

class Solution {
    public String longestCommonPrefix(String[] strs) {
        Arrays.sort(strs);

        String s1 = strs[0];
        String s2 = strs[strs.length - 1];

        int idx = 0;

        while (idx < s1.length() && idx < s2.length()) {
            if (s1.charAt(idx) == s2.charAt(idx)) {
                idx++;
            } else {
                break;
            }
        }

        return s1.substring(0, idx);
    }
}
```

#### Key Insight

Sorting reduces the problem to comparing just two strings instead of all of them. The first and last elements after sorting represent the maximum possible mismatch, so their common prefix guarantees correctness for the entire array.

---

## Key Concepts Covered

* Two-pointer technique
* String traversal and matching
* Handling edge cases in input formatting
* Efficient string construction using `StringBuilder`

---

## Summary

These problems reinforce essential string manipulation techniques that are frequently tested in coding interviews. Mastering these patterns helps in tackling more advanced problems involving parsing, pattern matching, and text processing.
