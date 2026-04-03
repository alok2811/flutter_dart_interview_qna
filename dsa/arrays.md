# 📌 Arrays (Top 10 Questions - Dart)

---

## 1. Two Sum (LeetCode 1)

**Problem:** Find two numbers such that they add up to target.

**Example:**  
Input: nums = [2,7,11,15], target = 9  
Output: [0,1]

**Dart Code:**
List<int> twoSum(List<int> nums, int target) {
final map = <int, int>{};

      for (int i = 0; i < nums.length; i++) {
        int diff = target - nums[i];

        if (map.containsKey(diff)) {
          return [map[diff]!, i];
        }

        map[nums[i]] = i;
      }

      return [];
    }

Time: O(n)

---

## 2. Best Time to Buy and Sell Stock (LeetCode 121)

**Example:**  
Input: [7,1,5,3,6,4]  
Output: 5

**Dart Code:**
int maxProfit(List<int> prices) {
int minPrice = prices[0];
int profit = 0;

      for (int price in prices) {
        if (price < minPrice) minPrice = price;

        int currentProfit = price - minPrice;
        if (currentProfit > profit) {
          profit = currentProfit;
        }
      }

      return profit;
    }

---

## 3. Merge Sorted Array (LeetCode 88)

**Example:**  
nums1 = [1,2,3,0,0,0], nums2 = [2,5,6]

**Dart Code:**
void merge(List<int> nums1, int m, List<int> nums2, int n) {
int i = m - 1;
int j = n - 1;
int k = m + n - 1;

      while (j >= 0) {
        if (i >= 0 && nums1[i] > nums2[j]) {
          nums1[k--] = nums1[i--];
        } else {
          nums1[k--] = nums2[j--];
        }
      }
    }

---

## 4. Contains Duplicate (LeetCode 217)

**Example:**  
[1,2,3,1] → true

**Dart Code:**
bool containsDuplicate(List<int> nums) {
final set = <int>{};

      for (int n in nums) {
        if (set.contains(n)) return true;
        set.add(n);
      }

      return false;
    }

---

## 5. Product of Array Except Self (LeetCode 238)

**Example:**  
[1,2,3,4] → [24,12,8,6]

**Dart Code:**
List<int> productExceptSelf(List<int> nums) {
int n = nums.length;
List<int> result = List.filled(n, 1);

      int left = 1;
      for (int i = 0; i < n; i++) {
        result[i] = left;
        left *= nums[i];
      }

      int right = 1;
      for (int i = n - 1; i >= 0; i--) {
        result[i] *= right;
        right *= nums[i];
      }

      return result;
    }

---

## 6. Maximum Subarray (LeetCode 53)

**Example:**  
[-2,1,-3,4,-1,2,1,-5,4] → 6

**Dart Code:**
int maxSubArray(List<int> nums) {
int current = nums[0];
int maxSum = nums[0];

      for (int i = 1; i < nums.length; i++) {
        current = current + nums[i] > nums[i]
            ? current + nums[i]
            : nums[i];

        if (current > maxSum) {
          maxSum = current;
        }
      }

      return maxSum;
    }

---

## 7. 3Sum (LeetCode 15)

**Example:**  
[-1,0,1,2,-1,-4]

**Dart Code:**
List<List<int>> threeSum(List<int> nums) {
nums.sort();
List<List<int>> result = [];

      for (int i = 0; i < nums.length - 2; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;

        int left = i + 1;
        int right = nums.length - 1;

        while (left < right) {
          int sum = nums[i] + nums[left] + nums[right];

          if (sum == 0) {
            result.add([nums[i], nums[left], nums[right]]);

            while (left < right && nums[left] == nums[left + 1]) left++;
            while (left < right && nums[right] == nums[right - 1]) right--;

            left++;
            right--;
          } else if (sum < 0) {
            left++;
          } else {
            right--;
          }
        }
      }

      return result;
    }

---

## 8. Merge Intervals (LeetCode 56)

**Example:**  
[[1,3],[2,6]] → [[1,6]]

**Dart Code:**
List<List<int>> mergeIntervals(List<List<int>> intervals) {
intervals.sort((a, b) => a[0].compareTo(b[0]));

      List<List<int>> result = [];

      for (var interval in intervals) {
        if (result.isEmpty || result.last[1] < interval[0]) {
          result.add(interval);
        } else {
          result.last[1] =
              result.last[1] > interval[1] ? result.last[1] : interval[1];
        }
      }

      return result;
    }

---

## 9. Container With Most Water (LeetCode 11)

**Example:**  
[1,8,6,2,5,4,8,3,7] → 49

**Dart Code:**
int maxArea(List<int> height) {
int left = 0;
int right = height.length - 1;
int maxArea = 0;

      while (left < right) {
        int h = height[left] < height[right]
            ? height[left]
            : height[right];

        int area = h * (right - left);

        if (area > maxArea) maxArea = area;

        if (height[left] < height[right]) {
          left++;
        } else {
          right--;
        }
      }

      return maxArea;
    }

---

## 10. Rotate Image (LeetCode 48)

**Example:**  
[[1,2,3],[4,5,6],[7,8,9]]

**Dart Code:**
void rotate(List<List<int>> matrix) {
int n = matrix.length;

      // transpose
      for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
          int temp = matrix[i][j];
          matrix[i][j] = matrix[j][i];
          matrix[j][i] = temp;
        }
      }

      // reverse rows
      for (var row in matrix) {
        row.reverse();
      }
    }

---

# 🎯 Key Patterns

- HashMap → Two Sum
- Two Pointer → 3Sum, Container
- Prefix/Suffix → Product array
- Kadane → Max Subarray
- Sorting + Merge → Intervals

---