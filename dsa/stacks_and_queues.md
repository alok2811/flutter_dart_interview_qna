# 📌 Stacks and Queues (Top 6 Questions - Dart)

---

## 1. Implement Queue using Stacks (LeetCode 232)

**Problem:**  
Implement a queue using only stacks.

**Example:**  
push(1), push(2), peek() → 1, pop() → 1, empty() → false

**Dart Code:**
class MyQueue {
List<int> input = [];
List<int> output = [];

      void push(int x) {
        input.add(x);
      }

      int pop() {
        peek();
        return output.removeLast();
      }

      int peek() {
        if (output.isEmpty) {
          while (input.isNotEmpty) {
            output.add(input.removeLast());
          }
        }
        return output.last;
      }

      bool empty() {
        return input.isEmpty && output.isEmpty;
      }
    }

**Approach:**  
Use one stack for incoming elements and one for outgoing elements.  
When removing or peeking, transfer elements only if needed.

**Time Complexity:**
- push → O(1)
- pop / peek → amortized O(1)

---

## 2. Implement Stack using Queues (LeetCode 225)

**Problem:**  
Implement a stack using queue operations.

**Example:**  
push(1), push(2), top() → 2, pop() → 2

**Dart Code:**
class MyStack {
List<int> queue = [];

      void push(int x) {
        queue.add(x);

        for (int i = 0; i < queue.length - 1; i++) {
          queue.add(queue.removeAt(0));
        }
      }

      int pop() {
        return queue.removeAt(0);
      }

      int top() {
        return queue[0];
      }

      bool empty() {
        return queue.isEmpty;
      }
    }

**Approach:**  
After every push, rotate queue so the newly added element comes to the front.

**Time Complexity:**
- push → O(n)
- pop → O(1)

---

## 3. Daily Temperatures (LeetCode 739)

**Problem:**  
For each day, find how many days you have to wait until a warmer temperature.

**Example:**  
Input: [73,74,75,71,69,72,76,73]  
Output: [1,1,4,2,1,1,0,0]

**Dart Code:**
List<int> dailyTemperatures(List<int> temperatures) {
List<int> result = List.filled(temperatures.length, 0);
List<int> stack = [];

      for (int i = 0; i < temperatures.length; i++) {
        while (stack.isNotEmpty &&
            temperatures[i] > temperatures[stack.last]) {
          int index = stack.removeLast();
          result[index] = i - index;
        }
        stack.add(i);
      }

      return result;
    }

**Approach:**  
Use a monotonic decreasing stack to keep indices of unresolved temperatures.

**Time Complexity:** O(n)

---

## 4. Next Greater Element I (LeetCode 496)

**Problem:**  
For each element in nums1, find the next greater element in nums2.

**Example:**  
nums1 = [4,1,2], nums2 = [1,3,4,2]  
Output: [-1,3,-1]

**Dart Code:**
List<int> nextGreaterElement(List<int> nums1, List<int> nums2) {
Map<int, int> nextGreater = {};
List<int> stack = [];

      for (int num in nums2) {
        while (stack.isNotEmpty && num > stack.last) {
          nextGreater[stack.removeLast()] = num;
        }
        stack.add(num);
      }

      while (stack.isNotEmpty) {
        nextGreater[stack.removeLast()] = -1;
      }

      return nums1.map((num) => nextGreater[num]!).toList();
    }

**Approach:**  
Use a monotonic stack to precompute the next greater element for every value in nums2.

**Time Complexity:** O(n)

---

## 5. Valid Parentheses (LeetCode 20)

**Problem:**  
Check if the parentheses string is valid.

**Example:**  
Input: "()[]{}"  
Output: true

**Dart Code:**
bool isValid(String s) {
List<String> stack = [];

      Map<String, String> pairs = {
        ')': '(',
        '}': '{',
        ']': '[',
      };

      for (String ch in s.split('')) {
        if (pairs.containsValue(ch)) {
          stack.add(ch);
        } else {
          if (stack.isEmpty || stack.removeLast() != pairs[ch]) {
            return false;
          }
        }
      }

      return stack.isEmpty;
    }

**Approach:**  
Push opening brackets into stack.  
For closing bracket, check top of stack.

**Time Complexity:** O(n)

---

## 6. Min Stack (LeetCode 155)

**Problem:**  
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

**Example:**  
push(-2), push(0), push(-3), getMin() → -3

**Dart Code:**
class MinStack {
List<int> stack = [];
List<int> minStack = [];

      void push(int val) {
        stack.add(val);

        if (minStack.isEmpty || val <= minStack.last) {
          minStack.add(val);
        }
      }

      void pop() {
        if (stack.removeLast() == minStack.last) {
          minStack.removeLast();
        }
      }

      int top() {
        return stack.last;
      }

      int getMin() {
        return minStack.last;
      }
    }

**Approach:**  
Maintain one normal stack and one min stack.  
The min stack stores the current minimums.

**Time Complexity:**
- push → O(1)
- pop → O(1)
- top → O(1)
- getMin → O(1)

---

# 🎯 Key Patterns

- Two stacks ↔ queue
- Queue rotation ↔ stack
- Monotonic stack → Daily Temperatures
- Monotonic stack → Next Greater Element
- Stack matching → Valid Parentheses
- Extra min stack → Min Stack

---