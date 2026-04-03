# Easy Coding Interview Questions (Dart)

A beginner-friendly collection of common coding interview questions with simple Dart solutions.

---

## 0. Frequency of Characters in a String

**Problem:** Find the frequency of each character in a given string.
**Example:**  
Input: `"hello"`  
Output: `h: 1, e: 1, l: 2, o: 1`
**Dart Code:**
```dart
Map<String, int> charFrequency(String s) {
  Map<String, int> freq = {};

  for (int i = 0; i < s.length; i++) {
    String char = s[i];
    if (freq.containsKey(char)) {
      freq[char] = freq[char]! + 1;
    } else {
      freq[char] = 1;
    }
  }

  return freq;
}
```
---

## 1. Palindrome Number

**Problem:** Check whether a number is a palindrome.

**Example:**  
Input: `121`  
Output: `true`

**Dart Code:**
```dart
bool isPalindromeNumber(int n) {
  if (n < 0) return false;

  int original = n;
  int reversed = 0;

  while (n > 0) {
    int digit = n % 10;
    reversed = reversed * 10 + digit;
    n ~/= 10;
  }

  return original == reversed;
}
```

---

## 2. Prime Number

**Problem:** Check whether a number is prime.

**Example:**  
Input: `13`  
Output: `true`

**Dart Code:**
```dart
bool isPrime(int n) {
  if (n <= 1) return false;

  for (int i = 2; i * i <= n; i++) {
    if (n % i == 0) return false;
  }

  return true;
}
```

---

## 3. Factorial of a Number

**Problem:** Find factorial of a number.

**Example:**  
Input: `5`  
Output: `120`

**Dart Code:**
```dart
int factorial(int n) {
  int result = 1;

  for (int i = 2; i <= n; i++) {
    result *= i;
  }

  return result;
}
```

---

## 4. Second Largest Element in Array

**Problem:** Find the second largest distinct element in an array.

**Example:**  
Input: `[10, 20, 4, 45, 99]`  
Output: `45`

**Dart Code:**
```dart
int? secondLargest(List<int> nums) {
  int? first;
  int? second;

  for (int num in nums) {
    if (first == null || num > first) {
      second = first;
      first = num;
    } else if (num != first && (second == null || num > second)) {
      second = num;
    }
  }

  return second;
}
```

---

## 5. Missing Number in Array

**Problem:** Find the missing number from `1` to `N`.

**Example:**  
Input: `[1, 2, 3, 5]`, `N = 5`  
Output: `4`

**Dart Code:**
```dart
int missingNumber(List<int> nums, int n) {
  int expectedSum = n * (n + 1) ~/ 2;
  int actualSum = nums.fold(0, (sum, num) => sum + num);
  return expectedSum - actualSum;
}
```

---

## 6. Reverse a String

**Problem:** Reverse a given string.

**Example:**  
Input: `"apple"`  
Output: `"elppa"`

**Dart Code:**
```dart
String reverseString(String s) {
  List<String> chars = s.split('');
  int left = 0;
  int right = chars.length - 1;

  while (left < right) {
    String temp = chars[left];
    chars[left] = chars[right];
    chars[right] = temp;
    left++;
    right--;
  }

  return chars.join();
}
```

---

## 7. Anagram Check

**Problem:** Check if two strings are anagrams.

**Example:**  
Input: `"listen", "silent"`  
Output: `true`

**Dart Code:**
```dart
bool isAnagram(String a, String b) {
  if (a.length != b.length) return false;

  List<String> aChars = a.toLowerCase().split('');
  List<String> bChars = b.toLowerCase().split('');

  aChars.sort();
  bChars.sort();

  return aChars.join() == bChars.join();
}
```

---

## 8. Fibonacci Series

**Problem:** Print first `N` terms of Fibonacci series.

**Example:**  
Input: `5`  
Output: `0 1 1 2 3`

**Dart Code:**
```dart
List<int> fibonacci(int n) {
  List<int> result = [];

  if (n >= 1) result.add(0);
  if (n >= 2) result.add(1);

  while (result.length < n) {
    int len = result.length;
    result.add(result[len - 1] + result[len - 2]);
  }

  return result;
}
```

---

## 9. Binary Search

**Problem:** Search an element in a sorted array.

**Example:**  
Input: `[1, 3, 5, 7, 9]`, target = `7`  
Output: `3`

**Dart Code:**
```dart
int binarySearch(List<int> nums, int target) {
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
```

---

## 10. Pattern Printing (Pyramid)

**Problem:** Print a star pyramid pattern.

**Example (n = 4):**
```text
   *
  ***
 *****
*******
```

**Dart Code:**
```dart
void printPyramid(int n) {
  for (int i = 1; i <= n; i++) {
    String spaces = ' ' * (n - i);
    String stars = '*' * (2 * i - 1);
    print(spaces + stars);
  }
}
```

---

# Extra Most-Asked Easy Questions

## 11. Frequency of Letter in a Word

**Problem:** Count frequency of each letter in a string like `"apple"`.

**Example:**  
Input: `"apple"`  
Output: `{a: 1, p: 2, l: 1, e: 1}`

**Dart Code:**
```dart
Map<String, int> letterFrequency(String s) {
  Map<String, int> freq = {};

  for (String ch in s.toLowerCase().split('')) {
    if (ch.trim().isEmpty) continue;
    freq[ch] = (freq[ch] ?? 0) + 1;
  }

  return freq;
}
```

---

## 12. Count Vowels in a String

**Problem:** Count vowels in a string.

**Example:**  
Input: `"apple"`  
Output: `2`

**Dart Code:**
```dart
int countVowels(String s) {
  Set<String> vowels = {'a', 'e', 'i', 'o', 'u'};
  int count = 0;

  for (String ch in s.toLowerCase().split('')) {
    if (vowels.contains(ch)) {
      count++;
    }
  }

  return count;
}
```

---

## 13. Sum of Digits

**Problem:** Find sum of digits of a number.

**Example:**  
Input: `1234`  
Output: `10`

**Dart Code:**
```dart
int sumOfDigits(int n) {
  int sum = 0;
  n = n.abs();

  while (n > 0) {
    sum += n % 10;
    n ~/= 10;
  }

  return sum;
}
```

---

## 14. Armstrong Number

**Problem:** Check whether a number is an Armstrong number.

**Example:**  
Input: `153`  
Output: `true`

**Dart Code:**
```dart
bool isArmstrong(int n) {
  String s = n.toString();
  int power = s.length;
  int sum = 0;
  int temp = n;

  while (temp > 0) {
    int digit = temp % 10;
    sum += digit.pow(power).toInt();
    temp ~/= 10;
  }

  return sum == n;
}
```

**Note:** Add this import for `pow`:
```dart
import 'dart:math';
```

---

## 15. Count Words in a Sentence

**Problem:** Count number of words in a sentence.

**Example:**  
Input: `"I love Dart"`  
Output: `3`

**Dart Code:**
```dart
int countWords(String s) {
  return s.trim().split(RegExp(r'\s+')).where((e) => e.isNotEmpty).length;
}
```

---

## 16. Largest Element in Array

**Problem:** Find largest element in an array.

**Example:**  
Input: `[3, 9, 2, 7]`  
Output: `9`

**Dart Code:**
```dart
int largestElement(List<int> nums) {
  int largest = nums[0];

  for (int num in nums) {
    if (num > largest) {
      largest = num;
    }
  }

  return largest;
}
```

---

## 17. Check Even or Odd

**Problem:** Check whether a number is even or odd.

**Example:**  
Input: `8`  
Output: `"Even"`

**Dart Code:**
```dart
String evenOrOdd(int n) {
  return n % 2 == 0 ? 'Even' : 'Odd';
}
```

---

## 18. Swap Two Numbers

**Problem:** Swap two numbers.

**Example:**  
Input: `a = 5, b = 7`  
Output: `a = 7, b = 5`

**Dart Code:**
```dart
void swapNumbers(int a, int b) {
  int temp = a;
  a = b;
  b = temp;

  print('a = $a, b = $b');
}
```

---

## 19. Check Palindrome String

**Problem:** Check whether a string is palindrome.

**Example:**  
Input: `"madam"`  
Output: `true`

**Dart Code:**
```dart
bool isPalindromeString(String s) {
  int left = 0;
  int right = s.length - 1;

  while (left < right) {
    if (s[left] != s[right]) return false;
    left++;
    right--;
  }

  return true;
}
```

---

## 20. Count Occurrence of One Character

**Problem:** Count how many times a character appears in a string.

**Example:**  
Input: `"apple", 'p'`  
Output: `2`

**Dart Code:**
```dart
int countChar(String s, String target) {
  int count = 0;

  for (String ch in s.split('')) {
    if (ch == target) count++;
  }

  return count;
}
```

---


## 21. Remove Duplicates from Array

**Problem:** Remove duplicate values from an array.

**Example:**  
Input: `[1, 2, 2, 3, 4, 4]`  
Output: `[1, 2, 3, 4]`

**Dart Code:**
```dart
List<int> removeDuplicates(List<int> nums) {
  return nums.toSet().toList();
}
```

---

## 22. Count Duplicate Elements in Array

**Problem:** Count frequency of each number in an array.

**Example:**  
Input: `[1, 2, 2, 3, 3, 3]`  
Output: `{1: 1, 2: 2, 3: 3}`

**Dart Code:**
```dart
Map<int, int> countDuplicates(List<int> nums) {
  Map<int, int> freq = {};

  for (int num in nums) {
    freq[num] = (freq[num] ?? 0) + 1;
  }

  return freq;
}
```

---

## 23. Find Duplicate Number

**Problem:** Find the first duplicate number in an array.

**Example:**  
Input: `[1, 3, 4, 2, 2]`  
Output: `2`

**Dart Code:**
```dart
int? findDuplicate(List<int> nums) {
  Set<int> seen = {};

  for (int num in nums) {
    if (seen.contains(num)) return num;
    seen.add(num);
  }

  return null;
}
```

---

## 24. Sort an Array in Ascending Order

**Problem:** Sort an array in ascending order.

**Example:**  
Input: `[5, 2, 9, 1]`  
Output: `[1, 2, 5, 9]`

**Dart Code:**
```dart
List<int> sortAscending(List<int> nums) {
  List<int> result = List.from(nums);
  result.sort();
  return result;
}
```

---

## 25. Sort an Array in Descending Order

**Problem:** Sort an array in descending order.

**Example:**  
Input: `[5, 2, 9, 1]`  
Output: `[9, 5, 2, 1]`

**Dart Code:**
```dart
List<int> sortDescending(List<int> nums) {
  List<int> result = List.from(nums);
  result.sort((a, b) => b.compareTo(a));
  return result;
}
```

---

## 26. Linear Search

**Problem:** Search an element in an unsorted array.

**Example:**  
Input: `[4, 8, 1, 6]`, target = `1`  
Output: `2`

**Dart Code:**
```dart
int linearSearch(List<int> nums, int target) {
  for (int i = 0; i < nums.length; i++) {
    if (nums[i] == target) return i;
  }

  return -1;
}
```

---

## 27. Array Rotation by One Position

**Problem:** Rotate array to the right by one position.

**Example:**  
Input: `[1, 2, 3, 4]`  
Output: `[4, 1, 2, 3]`

**Dart Code:**
```dart
List<int> rotateRightByOne(List<int> nums) {
  if (nums.isEmpty) return [];

  return [nums.last, ...nums.sublist(0, nums.length - 1)];
}
```

---

## 28. Reverse an Array

**Problem:** Reverse the elements of an array.

**Example:**  
Input: `[1, 2, 3, 4]`  
Output: `[4, 3, 2, 1]`

**Dart Code:**
```dart
List<int> reverseArray(List<int> nums) {
  List<int> result = List.from(nums);
  int left = 0;
  int right = result.length - 1;

  while (left < right) {
    int temp = result[left];
    result[left] = result[right];
    result[right] = temp;
    left++;
    right--;
  }

  return result;
}
```

---

## 29. Merge Two Arrays

**Problem:** Merge two arrays into one.

**Example:**  
Input: `[1, 2]`, `[3, 4]`  
Output: `[1, 2, 3, 4]`

**Dart Code:**
```dart
List<int> mergeArrays(List<int> a, List<int> b) {
  return [...a, ...b];
}
```

---

## 30. Find Minimum Element in Array

**Problem:** Find the smallest element in an array.

**Example:**  
Input: `[8, 3, 6, 1, 9]`  
Output: `1`

**Dart Code:**
```dart
int findMin(List<int> nums) {
  int minValue = nums[0];

  for (int num in nums) {
    if (num < minValue) {
      minValue = num;
    }
  }

  return minValue;
}
```

---

## 31. Find Maximum Element in Array

**Problem:** Find the largest element in an array.

**Example:**  
Input: `[8, 3, 6, 1, 9]`  
Output: `9`

**Dart Code:**
```dart
int findMax(List<int> nums) {
  int maxValue = nums[0];

  for (int num in nums) {
    if (num > maxValue) {
      maxValue = num;
    }
  }

  return maxValue;
}
```

---

## 32. Sum of Array Elements

**Problem:** Find sum of all elements in an array.

**Example:**  
Input: `[1, 2, 3, 4]`  
Output: `10`

**Dart Code:**
```dart
int sumOfArray(List<int> nums) {
  return nums.fold(0, (sum, num) => sum + num);
}
```

---

## 33. Average of Array Elements

**Problem:** Find average of all elements in an array.

**Example:**  
Input: `[2, 4, 6, 8]`  
Output: `5.0`

**Dart Code:**
```dart
double averageOfArray(List<int> nums) {
  int sum = nums.fold(0, (total, num) => total + num);
  return sum / nums.length;
}
```

---

## 34. Check if Array is Sorted

**Problem:** Check whether an array is sorted in ascending order.

**Example:**  
Input: `[1, 2, 3, 4]`  
Output: `true`

**Dart Code:**
```dart
bool isSorted(List<int> nums) {
  for (int i = 1; i < nums.length; i++) {
    if (nums[i] < nums[i - 1]) return false;
  }

  return true;
}
```

---

## 35. Find Common Elements in Two Arrays

**Problem:** Find common values between two arrays.

**Example:**  
Input: `[1, 2, 3, 4]`, `[3, 4, 5, 6]`  
Output: `[3, 4]`

**Dart Code:**
```dart
List<int> commonElements(List<int> a, List<int> b) {
  Set<int> setB = b.toSet();
  List<int> result = [];

  for (int num in a) {
    if (setB.contains(num) && !result.contains(num)) {
      result.add(num);
    }
  }

  return result;
}
```

---

## 36. Find Union of Two Arrays

**Problem:** Find all unique elements from two arrays.

**Example:**  
Input: `[1, 2, 3]`, `[3, 4, 5]`  
Output: `[1, 2, 3, 4, 5]`

**Dart Code:**
```dart
List<int> unionOfArrays(List<int> a, List<int> b) {
  return {...a, ...b}.toList();
}
```

---

## 37. Check Leap Year

**Problem:** Check whether a year is a leap year.

**Example:**  
Input: `2024`  
Output: `true`

**Dart Code:**
```dart
bool isLeapYear(int year) {
  return (year % 400 == 0) || (year % 4 == 0 && year % 100 != 0);
}
```

---

## 38. GCD of Two Numbers

**Problem:** Find greatest common divisor of two numbers.

**Example:**  
Input: `12, 18`  
Output: `6`

**Dart Code:**
```dart
int gcd(int a, int b) {
  while (b != 0) {
    int temp = b;
    b = a % b;
    a = temp;
  }

  return a.abs();
}
```

---

## 39. LCM of Two Numbers

**Problem:** Find least common multiple of two numbers.

**Example:**  
Input: `12, 18`  
Output: `36`

**Dart Code:**
```dart
int gcd(int a, int b) {
  while (b != 0) {
    int temp = b;
    b = a % b;
    a = temp;
  }

  return a.abs();
}

int lcm(int a, int b) {
  return (a * b).abs() ~/ gcd(a, b);
}
```

---

## 40. Check if Two Numbers are Equal Without Using ==

**Problem:** Check equality using subtraction or XOR idea.

**Example:**  
Input: `5, 5`  
Output: `true`

**Dart Code:**
```dart
bool areEqual(int a, int b) {
  return (a ^ b) == 0;
}
```

---

## 41. Matrix Addition

**Problem:** Add two matrices of same size.

**Example:**  
Input: `[[1,2],[3,4]]`, `[[5,6],[7,8]]`  
Output: `[[6,8],[10,12]]`

**Dart Code:**
```dart
List<List<int>> addMatrices(List<List<int>> a, List<List<int>> b) {
  int rows = a.length;
  int cols = a[0].length;

  List<List<int>> result =
      List.generate(rows, (_) => List.filled(cols, 0));

  for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
      result[i][j] = a[i][j] + b[i][j];
    }
  }

  return result;
}
```

---

## 42. Matrix Transpose

**Problem:** Find transpose of a matrix.

**Example:**  
Input: `[[1,2,3],[4,5,6]]`  
Output: `[[1,4],[2,5],[3,6]]`

**Dart Code:**
```dart
List<List<int>> transpose(List<List<int>> matrix) {
  int rows = matrix.length;
  int cols = matrix[0].length;

  List<List<int>> result =
      List.generate(cols, (_) => List.filled(rows, 0));

  for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
      result[j][i] = matrix[i][j];
    }
  }

  return result;
}
```

---

## 43. Count Digits in a Number

**Problem:** Count number of digits in an integer.

**Example:**  
Input: `12345`  
Output: `5`

**Dart Code:**
```dart
int countDigits(int n) {
  n = n.abs();

  if (n == 0) return 1;

  int count = 0;
  while (n > 0) {
    count++;
    n ~/= 10;
  }

  return count;
}
```

---

## 44. Check Perfect Number

**Problem:** Check whether a number is a perfect number.

**Example:**  
Input: `6`  
Output: `true`

**Dart Code:**
```dart
bool isPerfectNumber(int n) {
  if (n <= 1) return false;

  int sum = 1;

  for (int i = 2; i * i <= n; i++) {
    if (n % i == 0) {
      sum += i;
      if (i != n ~/ i) {
        sum += n ~/ i;
      }
    }
  }

  return sum == n;
}
```

---

## 45. Print Multiplication Table

**Problem:** Print multiplication table of a number.

**Example:**  
Input: `5`  
Output: `5 x 1 = 5 ... 5 x 10 = 50`

**Dart Code:**
```dart
void printTable(int n) {
  for (int i = 1; i <= 10; i++) {
    print('$n x $i = ${n * i}');
  }
}
```

---

## 46. Check if a String Contains Only Digits

**Problem:** Check whether a string contains only numeric characters.

**Example:**  
Input: `"12345"`  
Output: `true`

**Dart Code:**
```dart
bool containsOnlyDigits(String s) {
  if (s.isEmpty) return false;

  for (String ch in s.split('')) {
    if (ch.codeUnitAt(0) < 48 || ch.codeUnitAt(0) > 57) {
      return false;
    }
  }

  return true;
}
```

---

## 47. Remove Spaces from a String

**Problem:** Remove all spaces from a string.

**Example:**  
Input: `"i love dart"`  
Output: `"ilovedart"`

**Dart Code:**
```dart
String removeSpaces(String s) {
  return s.replaceAll(' ', '');
}
```

---

## 48. Convert Lowercase to Uppercase

**Problem:** Convert a string to uppercase.

**Example:**  
Input: `"apple"`  
Output: `"APPLE"`

**Dart Code:**
```dart
String toUpperCaseText(String s) {
  return s.toUpperCase();
}
```

---

## 49. Convert Uppercase to Lowercase

**Problem:** Convert a string to lowercase.

**Example:**  
Input: `"DART"`  
Output: `"dart"`

**Dart Code:**
```dart
String toLowerCaseText(String s) {
  return s.toLowerCase();
}
```

---

## 50. Find First Non-Repeating Character

**Problem:** Find the first character that appears only once.

**Example:**  
Input: `"swiss"`  
Output: `"w"`

**Dart Code:**
```dart
String? firstNonRepeatingChar(String s) {
  Map<String, int> freq = {};

  for (String ch in s.split('')) {
    freq[ch] = (freq[ch] ?? 0) + 1;
  }

  for (String ch in s.split('')) {
    if (freq[ch] == 1) return ch;
  }

  return null;
}
```

---

## 51. Find First Repeating Character

**Problem:** Find the first character that repeats in a string.

**Example:**  
Input: `"apple"`  
Output: `"p"`

**Dart Code:**
```dart
String? firstRepeatingChar(String s) {
  Set<String> seen = {};

  for (String ch in s.split('')) {
    if (seen.contains(ch)) return ch;
    seen.add(ch);
  }

  return null;
}
```

---

## 52. Count Uppercase and Lowercase Letters

**Problem:** Count uppercase and lowercase letters in a string.

**Example:**  
Input: `"ApPle"`  
Output: `uppercase = 2, lowercase = 3`

**Dart Code:**
```dart
Map<String, int> countUpperLower(String s) {
  int upper = 0;
  int lower = 0;

  for (String ch in s.split('')) {
    int code = ch.codeUnitAt(0);

    if (code >= 65 && code <= 90) {
      upper++;
    } else if (code >= 97 && code <= 122) {
      lower++;
    }
  }

  return {
    'uppercase': upper,
    'lowercase': lower,
  };
}
```

---

## 53. Remove Duplicate Characters from String

**Problem:** Remove repeated characters and keep first occurrence.

**Example:**  
Input: `"programming"`  
Output: `"progamin"`

**Dart Code:**
```dart
String removeDuplicateChars(String s) {
  Set<String> seen = {};
  String result = '';

  for (String ch in s.split('')) {
    if (!seen.contains(ch)) {
      seen.add(ch);
      result += ch;
    }
  }

  return result;
}
```

---

## 54. Toggle Case of Each Character

**Problem:** Convert uppercase to lowercase and lowercase to uppercase.

**Example:**  
Input: `"AbC"`  
Output: `"aBc"`

**Dart Code:**
```dart
String toggleCase(String s) {
  String result = '';

  for (String ch in s.split('')) {
    if (ch == ch.toUpperCase() && ch != ch.toLowerCase()) {
      result += ch.toLowerCase();
    } else if (ch == ch.toLowerCase() && ch != ch.toUpperCase()) {
      result += ch.toUpperCase();
    } else {
      result += ch;
    }
  }

  return result;
}
```

---

## 55. Replace Vowels with Special Character

**Problem:** Replace all vowels with `*`.

**Example:**  
Input: `"apple"`  
Output: `"*ppl*"`

**Dart Code:**
```dart
String replaceVowels(String s) {
  Set<String> vowels = {'a', 'e', 'i', 'o', 'u',
                        'A', 'E', 'I', 'O', 'U'};

  String result = '';

  for (String ch in s.split('')) {
    if (vowels.contains(ch)) {
      result += '*';
    } else {
      result += ch;
    }
  }

  return result;
}
```

---

## 56. Check if Two Strings are Rotations

**Problem:** Check if one string is rotation of another.

**Example:**  
Input: `"abcd", "cdab"`  
Output: `true`

**Dart Code:**
```dart
bool areRotations(String a, String b) {
  if (a.length != b.length) return false;
  return (a + a).contains(b);
}
```

---

## 57. Reverse Words in a Sentence

**Problem:** Reverse word order in a sentence.

**Example:**  
Input: `"I love Dart"`  
Output: `"Dart love I"`

**Dart Code:**
```dart
String reverseWords(String s) {
  List<String> words =
      s.trim().split(RegExp(r'\s+'));
  return words.reversed.join(' ');
}
```

---

## 58. Check if a Number is Positive, Negative, or Zero

**Problem:** Classify a number.

**Example:**  
Input: `-5`  
Output: `"Negative"`

**Dart Code:**
```dart
String numberType(int n) {
  if (n > 0) return 'Positive';
  if (n < 0) return 'Negative';
  return 'Zero';
}
```

---

## 59. Reverse Digits of a Number

**Problem:** Reverse digits of a number.

**Example:**  
Input: `1234`  
Output: `4321`

**Dart Code:**
```dart
int reverseNumber(int n) {
  int reversed = 0;
  int num = n.abs();

  while (num > 0) {
    reversed = reversed * 10 + num % 10;
    num ~/= 10;
  }

  return n < 0 ? -reversed : reversed;
}
```

---

## 60. Check if Number is Armstrong Using String-Free Logic

**Problem:** Check Armstrong number without converting digits repeatedly by string operations.

**Example:**  
Input: `153`  
Output: `true`

**Dart Code:**
```dart
import 'dart:math';

bool isArmstrongNumber(int n) {
  int temp = n;
  int digits = 0;

  while (temp > 0) {
    digits++;
    temp ~/= 10;
  }

  temp = n;
  int sum = 0;

  while (temp > 0) {
    int digit = temp % 10;
    sum += pow(digit, digits).toInt();
    temp ~/= 10;
  }

  return sum == n;
}
```

---

## 61. Generate All Factors of a Number

**Problem:** Print all factors of a number.

**Example:**  
Input: `12`  
Output: `[1, 2, 3, 4, 6, 12]`

**Dart Code:**
```dart
List<int> factors(int n) {
  List<int> result = [];

  for (int i = 1; i <= n; i++) {
    if (n % i == 0) {
      result.add(i);
    }
  }

  return result;
}
```

---

## 62. Check if Number is Perfect Square

**Problem:** Check whether a number is a perfect square.

**Example:**  
Input: `25`  
Output: `true`

**Dart Code:**
```dart
bool isPerfectSquare(int n) {
  if (n < 0) return false;

  for (int i = 0; i * i <= n; i++) {
    if (i * i == n) return true;
  }

  return false;
}
```

---

## 63. Decimal to Binary

**Problem:** Convert decimal number to binary string.

**Example:**  
Input: `10`  
Output: `"1010"`

**Dart Code:**
```dart
String decimalToBinary(int n) {
  if (n == 0) return '0';

  String result = '';
  int num = n;

  while (num > 0) {
    result = '${num % 2}$result';
    num ~/= 2;
  }

  return result;
}
```

---

## 64. Binary to Decimal

**Problem:** Convert binary string to decimal number.

**Example:**  
Input: `"1010"`  
Output: `10`

**Dart Code:**
```dart
int binaryToDecimal(String binary) {
  int result = 0;

  for (String bit in binary.split('')) {
    result = result * 2 + int.parse(bit);
  }

  return result;
}
```

---

## 65. Check if Number is Power of Two

**Problem:** Check whether a number is power of 2.

**Example:**  
Input: `16`  
Output: `true`

**Dart Code:**
```dart
bool isPowerOfTwo(int n) {
  if (n <= 0) return false;

  while (n % 2 == 0) {
    n ~/= 2;
  }

  return n == 1;
}
```

---

## 66. Recursive Factorial

**Problem:** Find factorial using recursion.

**Example:**  
Input: `5`  
Output: `120`

**Dart Code:**
```dart
int factorialRecursive(int n) {
  if (n <= 1) return 1;
  return n * factorialRecursive(n - 1);
}
```

---

## 67. Recursive Fibonacci

**Problem:** Find nth Fibonacci number using recursion.

**Example:**  
Input: `6`  
Output: `8`

**Dart Code:**
```dart
int fibonacciRecursive(int n) {
  if (n == 0) return 0;
  if (n == 1) return 1;

  return fibonacciRecursive(n - 1) +
         fibonacciRecursive(n - 2);
}
```

---

## 68. Sum of First N Natural Numbers

**Problem:** Find sum from 1 to N.

**Example:**  
Input: `5`  
Output: `15`

**Dart Code:**
```dart
int sumNatural(int n) {
  return n * (n + 1) ~/ 2;
}
```

---

## 69. Check if a String Starts and Ends with Same Character

**Problem:** Check whether first and last character are same.

**Example:**  
Input: `"level"`  
Output: `true`

**Dart Code:**
```dart
bool sameStartEnd(String s) {
  if (s.isEmpty) return false;
  return s[0] == s[s.length - 1];
}
```

---

## 70. Print Right Triangle Pattern

**Problem:** Print right triangle star pattern.

**Example (n = 4):**
```text
*
**
***
****
```

**Dart Code:**
```dart
void printRightTriangle(int n) {
  for (int i = 1; i <= n; i++) {
    print('*' * i);
  }
}
```

# Quick Interview Tips

- Start with brute-force if needed, then improve.
- Always handle edge cases like empty string, null-like cases, duplicates, and negative numbers.
- For easy questions, keep code simple and readable.
- In interviews, explain your logic before writing code.

---
