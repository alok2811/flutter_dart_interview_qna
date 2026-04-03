# 📌 Strings (Top 10 Questions - Dart)

---

## 1. Valid Parentheses (LeetCode 20)

**Problem:** Check if parentheses are valid.

**Example:**  
Input: "()[]{}" → true

**Dart Code:**
bool isValid(String s) {
List<String> stack = [];

      Map<String, String> map = {
        ')': '(',
        '}': '{',
        ']': '['
      };

      for (var char in s.split('')) {
        if (map.containsValue(char)) {
          stack.add(char);
        } else {
          if (stack.isEmpty || stack.removeLast() != map[char]) {
            return false;
          }
        }
      }

      return stack.isEmpty;
    }

---

## 2. Valid Palindrome (LeetCode 125)

**Example:**  
"A man, a plan, a canal: Panama" → true

**Dart Code:**
bool isPalindrome(String s) {
String clean = s
.replaceAll(RegExp(r'[^a-zA-Z0-9]'), '')
.toLowerCase();

      int left = 0;
      int right = clean.length - 1;

      while (left < right) {
        if (clean[left] != clean[right]) return false;
        left++;
        right--;
      }

      return true;
    }

---

## 3. Valid Anagram (LeetCode 242)

**Example:**  
"anagram", "nagaram" → true

**Dart Code:**
bool isAnagram(String s, String t) {
if (s.length != t.length) return false;

      Map<String, int> count = {};

      for (var char in s.split('')) {
        count[char] = (count[char] ?? 0) + 1;
      }

      for (var char in t.split('')) {
        if (!count.containsKey(char) || count[char] == 0) {
          return false;
        }
        count[char] = count[char]! - 1;
      }

      return true;
    }

---

## 4. Group Anagrams (LeetCode 49)

**Example:**  
["eat","tea","tan","ate","nat","bat"]

**Dart Code:**
List<List<String>> groupAnagrams(List<String> strs) {
Map<String, List<String>> map = {};

      for (var str in strs) {
        List<char> chars = str.split('');
        chars.sort();
        String key = chars.join();

        map.putIfAbsent(key, () => []);
        map[key]!.add(str);
      }

      return map.values.toList();
    }

---

## 5. Longest Palindromic Substring (LeetCode 5)

**Example:**  
"babad" → "bab"

**Dart Code:**
String longestPalindrome(String s) {
if (s.isEmpty) return "";

      int start = 0, end = 0;

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

---

## 6. Minimum Window Substring (LeetCode 76)

**Example:**  
s = "ADOBECODEBANC", t = "ABC" → "BANC"

**Dart Code:**
String minWindow(String s, String t) {
if (t.isEmpty) return "";

      Map<String, int> need = {};
      for (var c in t.split('')) {
        need[c] = (need[c] ?? 0) + 1;
      }

      int have = 0, needCount = need.length;
      Map<String, int> window = {};

      int left = 0;
      int minLen = 1 << 30;
      int start = 0;

      for (int right = 0; right < s.length; right++) {
        String c = s[right];
        window[c] = (window[c] ?? 0) + 1;

        if (need.containsKey(c) && window[c] == need[c]) {
          have++;
        }

        while (have == needCount) {
          if (right - left + 1 < minLen) {
            minLen = right - left + 1;
            start = left;
          }

          String leftChar = s[left];
          window[leftChar] = window[leftChar]! - 1;

          if (need.containsKey(leftChar) &&
              window[leftChar]! < need[leftChar]!) {
            have--;
          }

          left++;
        }
      }

      return minLen == 1 << 30
          ? ""
          : s.substring(start, start + minLen);
    }

---

## 7. Find First Occurrence (LeetCode 28)

**Example:**  
"hello", "ll" → 2

**Dart Code:**
int strStr(String haystack, String needle) {
return haystack.indexOf(needle);
}

---

## 8. String Compression (LeetCode 443)

**Example:**  
["a","a","b","b","c","c","c"] → ["a","2","b","2","c","3"]

**Dart Code:**
int compress(List<String> chars) {
int index = 0;
int i = 0;

      while (i < chars.length) {
        String current = chars[i];
        int count = 0;

        while (i < chars.length && chars[i] == current) {
          i++;
          count++;
        }

        chars[index++] = current;

        if (count > 1) {
          for (var c in count.toString().split('')) {
            chars[index++] = c;
          }
        }
      }

      return index;
    }

---

## 9. Longest Common Prefix (LeetCode 14)

**Example:**  
["flower","flow","flight"] → "fl"

**Dart Code:**
String longestCommonPrefix(List<String> strs) {
if (strs.isEmpty) return "";

      String prefix = strs[0];

      for (int i = 1; i < strs.length; i++) {
        while (!strs[i].startsWith(prefix)) {
          prefix = prefix.substring(0, prefix.length - 1);
          if (prefix.isEmpty) return "";
        }
      }

      return prefix;
    }

---

## 10. Repeated Substring Pattern (LeetCode 459)

**Example:**  
"abab" → true

**Dart Code:**
bool repeatedSubstringPattern(String s) {
String doubled = s + s;
return doubled.substring(1, doubled.length - 1).contains(s);
}

---

# 🎯 Key Patterns

- Stack → Valid Parentheses
- Two Pointer → Palindrome
- HashMap → Anagram
- Sliding Window → Min Window
- Expand Around Center → Palindrome
- String Tricks → Repeat pattern

---