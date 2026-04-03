# 📌 Dynamic Programming (Top 10 Questions - Dart)

---

## 1. Climbing Stairs (LeetCode 70)

**Problem:**  
You can climb 1 or 2 steps at a time. Find how many distinct ways to reach the top.

**Example:**  
Input: n = 3  
Output: 3  
Explanation: [1+1+1], [1+2], [2+1]

**Dart Code:**
int climbStairs(int n) {
if (n <= 2) return n;

      int first = 1;
      int second = 2;

      for (int i = 3; i <= n; i++) {
        int current = first + second;
        first = second;
        second = current;
      }

      return second;
    }

**Approach:**  
This is like Fibonacci.  
Ways to reach step `n` = ways to reach `n-1` + ways to reach `n-2`.

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

---

## 2. House Robber (LeetCode 198)

**Problem:**  
You cannot rob two adjacent houses. Find the maximum money you can rob.

**Example:**  
Input: [2,7,9,3,1]  
Output: 12

**Dart Code:**
int rob(List<int> nums) {
int prev2 = 0;
int prev1 = 0;

      for (int money in nums) {
        int current = (prev2 + money > prev1) ? prev2 + money : prev1;
        prev2 = prev1;
        prev1 = current;
      }

      return prev1;
    }

**Approach:**  
At each house:
- rob it + value from 2 houses before
- or skip it and keep previous max

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

---

## 3. Coin Change (LeetCode 322)

**Problem:**  
Given coins of different values and a target amount, find the minimum number of coins needed.

**Example:**  
Input: coins = [1,2,5], amount = 11  
Output: 3  
Explanation: 5 + 5 + 1

**Dart Code:**
int coinChange(List<int> coins, int amount) {
List<int> dp = List.filled(amount + 1, amount + 1);
dp[0] = 0;

      for (int i = 1; i <= amount; i++) {
        for (int coin in coins) {
          if (coin <= i) {
            int candidate = dp[i - coin] + 1;
            if (candidate < dp[i]) {
              dp[i] = candidate;
            }
          }
        }
      }

      return dp[amount] > amount ? -1 : dp[amount];
    }

**Approach:**  
Build answer from smaller amounts.  
`dp[i]` = minimum coins needed to make amount `i`.

**Time Complexity:** O(amount × number of coins)  
**Space Complexity:** O(amount)

---

## 4. Longest Increasing Subsequence (LeetCode 300)

**Problem:**  
Find the length of the longest strictly increasing subsequence.

**Example:**  
Input: [10,9,2,5,3,7,101,18]  
Output: 4  
Explanation: [2,3,7,101]

**Dart Code:**
int lengthOfLIS(List<int> nums) {
if (nums.isEmpty) return 0;

      List<int> dp = List.filled(nums.length, 1);
      int maxLen = 1;

      for (int i = 1; i < nums.length; i++) {
        for (int j = 0; j < i; j++) {
          if (nums[i] > nums[j] && dp[j] + 1 > dp[i]) {
            dp[i] = dp[j] + 1;
          }
        }

        if (dp[i] > maxLen) {
          maxLen = dp[i];
        }
      }

      return maxLen;
    }

**Approach:**  
For each index, check all previous smaller values and extend the subsequence.

**Time Complexity:** O(n²)  
**Space Complexity:** O(n)

---

## 5. Longest Common Subsequence (LeetCode 1143)

**Problem:**  
Find the length of the longest common subsequence between two strings.

**Example:**  
Input: text1 = "abcde", text2 = "ace"  
Output: 3

**Dart Code:**
int longestCommonSubsequence(String text1, String text2) {
int m = text1.length;
int n = text2.length;

      List<List<int>> dp =
          List.generate(m + 1, (_) => List.filled(n + 1, 0));

      for (int i = m - 1; i >= 0; i--) {
        for (int j = n - 1; j >= 0; j--) {
          if (text1[i] == text2[j]) {
            dp[i][j] = 1 + dp[i + 1][j + 1];
          } else {
            dp[i][j] = dp[i + 1][j] > dp[i][j + 1]
                ? dp[i + 1][j]
                : dp[i][j + 1];
          }
        }
      }

      return dp[0][0];
    }

**Approach:**  
If characters match, take 1 + diagonal.  
Otherwise, take max of skipping one character from either string.

**Time Complexity:** O(m × n)  
**Space Complexity:** O(m × n)

---

## 6. Unique Paths (LeetCode 62)

**Problem:**  
A robot starts at top-left and can move only right or down. Find total unique paths to bottom-right.

**Example:**  
Input: m = 3, n = 7  
Output: 28

**Dart Code:**
int uniquePaths(int m, int n) {
List<List<int>> dp =
List.generate(m, (_) => List.filled(n, 1));

      for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
          dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
        }
      }

      return dp[m - 1][n - 1];
    }

**Approach:**  
Ways to reach any cell = ways from top + ways from left.

**Time Complexity:** O(m × n)  
**Space Complexity:** O(m × n)

---

## 7. Longest Palindromic Substring (LeetCode 5)

**Problem:**  
Find the longest palindromic substring.

**Example:**  
Input: "babad"  
Output: "bab"

**Dart Code:**
String longestPalindrome(String s) {
if (s.isEmpty) return "";

      int start = 0;
      int end = 0;

      int expand(int left, int right) {
        while (left >= 0 &&
            right < s.length &&
            s[left] == s[right]) {
          left--;
          right++;
        }
        return right - left - 1;
      }

      for (int i = 0; i < s.length; i++) {
        int len1 = expand(i, i);
        int len2 = expand(i, i + 1);
        int len = len1 > len2 ? len1 : len2;

        if (len > end - start) {
          start = i - (len - 1) ~/ 2;
          end = i + len ~/ 2;
        }
      }

      return s.substring(start, end + 1);
    }

**Approach:**  
Try every index as center and expand outward.

**Time Complexity:** O(n²)  
**Space Complexity:** O(1)

---

## 8. Maximum Length of Repeated Subarray (LeetCode 718)

**Problem:**  
Find the maximum length of a subarray that appears in both arrays.

**Example:**  
Input: nums1 = [1,2,3,2,1], nums2 = [3,2,1,4,7]  
Output: 3

**Dart Code:**
int findLength(List<int> nums1, List<int> nums2) {
int m = nums1.length;
int n = nums2.length;

      List<List<int>> dp =
          List.generate(m + 1, (_) => List.filled(n + 1, 0));

      int maxLen = 0;

      for (int i = m - 1; i >= 0; i--) {
        for (int j = n - 1; j >= 0; j--) {
          if (nums1[i] == nums2[j]) {
            dp[i][j] = 1 + dp[i + 1][j + 1];
            if (dp[i][j] > maxLen) {
              maxLen = dp[i][j];
            }
          }
        }
      }

      return maxLen;
    }

**Approach:**  
If elements match, extend the common subarray from next indices.

**Time Complexity:** O(m × n)  
**Space Complexity:** O(m × n)

---

## 9. Partition Equal Subset Sum (LeetCode 416)

**Problem:**  
Check if array can be divided into two subsets with equal sum.

**Example:**  
Input: [1,5,11,5]  
Output: true

**Dart Code:**
bool canPartition(List<int> nums) {
int total = nums.fold(0, (sum, num) => sum + num);

      if (total % 2 != 0) return false;

      int target = total ~/ 2;
      List<bool> dp = List.filled(target + 1, false);
      dp[0] = true;

      for (int num in nums) {
        for (int i = target; i >= num; i--) {
          dp[i] = dp[i] || dp[i - num];
        }
      }

      return dp[target];
    }

**Approach:**  
Convert into subset sum problem:
Can we make sum = total / 2 ?

**Time Complexity:** O(n × target)  
**Space Complexity:** O(target)

---

## 10. Maximum Subarray (LeetCode 53)

**Problem:**  
Find the contiguous subarray with the largest sum.

**Example:**  
Input: [-2,1,-3,4,-1,2,1,-5,4]  
Output: 6  
Explanation: [4,-1,2,1]

**Dart Code:**
int maxSubArray(List<int> nums) {
int currentSum = nums[0];
int maxSum = nums[0];

      for (int i = 1; i < nums.length; i++) {
        currentSum = (nums[i] > currentSum + nums[i])
            ? nums[i]
            : currentSum + nums[i];

        if (currentSum > maxSum) {
          maxSum = currentSum;
        }
      }

      return maxSum;
    }

**Approach:**  
At each position:
- start new subarray
- or continue previous one

This is Kadane’s Algorithm.

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

---

# 🎯 Key Patterns

- Fibonacci DP → Climbing Stairs
- Pick / skip → House Robber
- Unbounded choice → Coin Change
- Compare previous states → LIS
- 2D DP table → LCS / Repeated Subarray
- Grid DP → Unique Paths
- Subset sum DP → Partition Equal Subset Sum
- Kadane’s Algorithm → Maximum Subarray

---