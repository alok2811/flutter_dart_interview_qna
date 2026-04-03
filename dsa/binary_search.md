# 📌 Binary Search (Top 6 Questions - Dart)

---

## 1. Binary Search (LeetCode 704)

**Problem:**  
Given a sorted array and a target, return its index. If not found, return -1.

**Example:**  
Input: nums = [-1,0,3,5,9,12], target = 9  
Output: 4

**Dart Code:**
int search(List<int> nums, int target) {
int left = 0;
int right = nums.length - 1;

      while (left <= right) {
        int mid = left + (right - left) ~/ 2;

        if (nums[mid] == target) return mid;

        if (nums[mid] < target) {
          left = mid + 1;
        } else {
          right = mid - 1;
        }
      }

      return -1;
    }

**Approach:**  
Keep checking the middle element and remove half of the search space each time.

**Time Complexity:** O(log n)

---

## 2. Find First and Last Position of Element in Sorted Array (LeetCode 34)

**Problem:**  
Find the starting and ending index of a target value in a sorted array.

**Example:**  
Input: nums = [5,7,7,8,8,10], target = 8  
Output: [3,4]

**Dart Code:**
List<int> searchRange(List<int> nums, int target) {
int first = findBound(nums, target, true);
int last = findBound(nums, target, false);
return [first, last];
}

    int findBound(List<int> nums, int target, bool isFirst) {
      int left = 0;
      int right = nums.length - 1;
      int bound = -1;

      while (left <= right) {
        int mid = left + (right - left) ~/ 2;

        if (nums[mid] == target) {
          bound = mid;
          if (isFirst) {
            right = mid - 1;
          } else {
            left = mid + 1;
          }
        } else if (nums[mid] < target) {
          left = mid + 1;
        } else {
          right = mid - 1;
        }
      }

      return bound;
    }

**Approach:**  
Run binary search twice:
- once for first occurrence
- once for last occurrence

**Time Complexity:** O(log n)

---

## 3. Search a 2D Matrix (LeetCode 74)

**Problem:**  
Search a target in a matrix where:
- each row is sorted
- first element of each row is greater than last element of previous row

**Example:**  
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3  
Output: true

**Dart Code:**
bool searchMatrix(List<List<int>> matrix, int target) {
int rows = matrix.length;
int cols = matrix[0].length;

      int left = 0;
      int right = rows * cols - 1;

      while (left <= right) {
        int mid = left + (right - left) ~/ 2;
        int value = matrix[mid ~/ cols][mid % cols];

        if (value == target) return true;

        if (value < target) {
          left = mid + 1;
        } else {
          right = mid - 1;
        }
      }

      return false;
    }

**Approach:**  
Treat the matrix like a flattened sorted array.

**Time Complexity:** O(log(m × n))

---

## 4. Search in Rotated Sorted Array (LeetCode 33)

**Problem:**  
Search target in a rotated sorted array with unique values.

**Example:**  
Input: nums = [4,5,6,7,0,1,2], target = 0  
Output: 4

**Dart Code:**
int searchRotated(List<int> nums, int target) {
int left = 0;
int right = nums.length - 1;

      while (left <= right) {
        int mid = left + (right - left) ~/ 2;

        if (nums[mid] == target) return mid;

        if (nums[left] <= nums[mid]) {
          if (nums[left] <= target && target < nums[mid]) {
            right = mid - 1;
          } else {
            left = mid + 1;
          }
        } else {
          if (nums[mid] < target && target <= nums[right]) {
            left = mid + 1;
          } else {
            right = mid - 1;
          }
        }
      }

      return -1;
    }

**Approach:**  
At least one half is always sorted.  
Decide whether target lies in the sorted half.

**Time Complexity:** O(log n)

---

## 5. Search in Rotated Sorted Array II (LeetCode 81)

**Problem:**  
Search target in a rotated sorted array that may contain duplicates.

**Example:**  
Input: nums = [2,5,6,0,0,1,2], target = 0  
Output: true

**Dart Code:**
bool searchRotatedWithDuplicates(List<int> nums, int target) {
int left = 0;
int right = nums.length - 1;

      while (left <= right) {
        int mid = left + (right - left) ~/ 2;

        if (nums[mid] == target) return true;

        if (nums[left] == nums[mid] && nums[mid] == nums[right]) {
          left++;
          right--;
        } else if (nums[left] <= nums[mid]) {
          if (nums[left] <= target && target < nums[mid]) {
            right = mid - 1;
          } else {
            left = mid + 1;
          }
        } else {
          if (nums[mid] < target && target <= nums[right]) {
            left = mid + 1;
          } else {
            right = mid - 1;
          }
        }
      }

      return false;
    }

**Approach:**  
Same as rotated binary search, but when duplicates block the decision, shrink both ends.

**Time Complexity:**  
Average: O(log n)  
Worst case: O(n)

---

## 6. Find Peak Element (LeetCode 162)

**Problem:**  
Find a peak element. A peak is greater than its neighbors.

**Example:**  
Input: nums = [1,2,3,1]  
Output: 2

**Dart Code:**
int findPeakElement(List<int> nums) {
int left = 0;
int right = nums.length - 1;

      while (left < right) {
        int mid = left + (right - left) ~/ 2;

        if (nums[mid] < nums[mid + 1]) {
          left = mid + 1;
        } else {
          right = mid;
        }
      }

      return left;
    }

**Approach:**  
If mid is smaller than next element, peak must exist on the right side.  
Otherwise, peak is on the left side including mid.

**Time Complexity:** O(log n)

---

# 🎯 Key Patterns

- Classic binary search → exact match
- Modified binary search → first / last occurrence
- Flattened indexing → 2D matrix
- Sorted half detection → rotated array
- Duplicate handling → shrink boundaries
- Slope-based search → peak element

---