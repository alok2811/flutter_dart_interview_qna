# 📌 Bit Manipulation (Top 4 Questions - Dart)

---

## 1. Single Number (LeetCode 136)

**Problem:**  
Every element appears twice except one. Find that single number.

**Example:**  
Input: [4,1,2,1,2]  
Output: 4

**Dart Code:**
int singleNumber(List<int> nums) {
int result = 0;

      for (int num in nums) {
        result ^= num;
      }

      return result;
    }

**Approach:**  
XOR properties:
- a ^ a = 0
- a ^ 0 = a

So all duplicates cancel out, leaving the single number.

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

---

## 2. Reverse Bits (LeetCode 190)

**Problem:**  
Reverse bits of a 32-bit unsigned integer.

**Example:**  
Input: 00000010100101000001111010011100  
Output: 00111001011110000010100101000000

**Dart Code:**
int reverseBits(int n) {
int result = 0;

      for (int i = 0; i < 32; i++) {
        result <<= 1;
        result |= (n & 1);
        n >>= 1;
      }

      return result;
    }

**Approach:**  
Shift result left and add last bit of n, then shift n right.

**Time Complexity:** O(1)  
**Space Complexity:** O(1)

---

## 3. Number of 1 Bits (LeetCode 191)

**Problem:**  
Count number of set bits (1s) in an integer.

**Example:**  
Input: 11 (binary 1011)  
Output: 3

**Dart Code:**
int hammingWeight(int n) {
int count = 0;

      while (n != 0) {
        count += n & 1;
        n >>= 1;
      }

      return count;
    }

**Approach:**  
Check last bit using `n & 1`, then shift right.

**Time Complexity:** O(1)  
**Space Complexity:** O(1)

---

## 4. Missing Number (LeetCode 268)

**Problem:**  
Find the missing number in range [0, n].

**Example:**  
Input: [3,0,1]  
Output: 2

**Dart Code (XOR Approach):**
int missingNumber(List<int> nums) {
int result = nums.length;

      for (int i = 0; i < nums.length; i++) {
        result ^= i ^ nums[i];
      }

      return result;
    }

**Approach:**  
XOR all indices and values → remaining is missing number.

**Alternative (Sum Formula):**
int missingNumberSum(List<int> nums) {
int n = nums.length;
int expected = n * (n + 1) ~/ 2;

      int actual = nums.fold(0, (sum, num) => sum + num);

      return expected - actual;
    }

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

---

# 🎯 Key Patterns

- XOR → Single Number, Missing Number
- Bit Shift → Reverse Bits
- Bit Check → Count set bits
- Math vs Bit → Multiple approaches

---