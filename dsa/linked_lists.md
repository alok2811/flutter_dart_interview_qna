# 📌 Linked List (Top Questions - Dart)

---

## Definition

    class ListNode {
      int val;
      ListNode? next;

      ListNode(this.val, [this.next]);
    }

---

## 1. Reverse Linked List (LeetCode 206)

**Example:**  
1 → 2 → 3 → 4 → null  
Output: 4 → 3 → 2 → 1 → null

**Dart Code:**
ListNode? reverseList(ListNode? head) {
ListNode? prev;
ListNode? curr = head;

      while (curr != null) {
        ListNode? next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
      }

      return prev;
    }

---

## 2. Merge Two Sorted Lists (LeetCode 21)

**Example:**  
[1,2,4], [1,3,4] → [1,1,2,3,4,4]

**Dart Code:**
ListNode? mergeTwoLists(ListNode? l1, ListNode? l2) {
ListNode dummy = ListNode(0);
ListNode current = dummy;

      while (l1 != null && l2 != null) {
        if (l1.val < l2.val) {
          current.next = l1;
          l1 = l1.next;
        } else {
          current.next = l2;
          l2 = l2.next;
        }
        current = current.next!;
      }

      current.next = l1 ?? l2;

      return dummy.next;
    }

---

## 3. Remove Nth Node From End (LeetCode 19)

**Example:**  
1 → 2 → 3 → 4 → 5, n = 2  
Output: 1 → 2 → 3 → 5

**Dart Code:**
ListNode? removeNthFromEnd(ListNode? head, int n) {
ListNode dummy = ListNode(0, head);
ListNode? fast = dummy;
ListNode? slow = dummy;

      for (int i = 0; i <= n; i++) {
        fast = fast!.next;
      }

      while (fast != null) {
        fast = fast.next;
        slow = slow!.next;
      }

      slow!.next = slow.next!.next;

      return dummy.next;
    }

---

## 4. Linked List Cycle (LeetCode 141)

**Example:**  
Check if cycle exists → true/false

**Dart Code:**
bool hasCycle(ListNode? head) {
ListNode? slow = head;
ListNode? fast = head;

      while (fast != null && fast.next != null) {
        slow = slow!.next;
        fast = fast.next!.next;

        if (slow == fast) return true;
      }

      return false;
    }

---

## 5. Add Two Numbers (LeetCode 2)

**Example:**  
[2,4,3] + [5,6,4] → [7,0,8]

**Dart Code:**
ListNode? addTwoNumbers(ListNode? l1, ListNode? l2) {
ListNode dummy = ListNode(0);
ListNode current = dummy;

      int carry = 0;

      while (l1 != null || l2 != null || carry != 0) {
        int sum = carry;

        if (l1 != null) {
          sum += l1.val;
          l1 = l1.next;
        }

        if (l2 != null) {
          sum += l2.val;
          l2 = l2.next;
        }

        carry = sum ~/ 10;

        current.next = ListNode(sum % 10);
        current = current.next!;
      }

      return dummy.next;
    }

---

## 6. Intersection of Two Linked Lists (LeetCode 160)

**Example:**  
Return intersection node

**Dart Code:**
ListNode? getIntersectionNode(ListNode? headA, ListNode? headB) {
if (headA == null || headB == null) return null;

      ListNode? a = headA;
      ListNode? b = headB;

      while (a != b) {
        a = (a == null) ? headB : a.next;
        b = (b == null) ? headA : b.next;
      }

      return a;
    }

---

## 7. Palindrome Linked List (LeetCode 234)

**Example:**  
1 → 2 → 2 → 1 → true

**Dart Code:**
bool isPalindrome(ListNode? head) {
List<int> values = [];

      while (head != null) {
        values.add(head.val);
        head = head.next;
      }

      int left = 0;
      int right = values.length - 1;

      while (left < right) {
        if (values[left] != values[right]) return false;
        left++;
        right--;
      }

      return true;
    }

---

## 8. Reverse Nodes in k-Group (LeetCode 25)

**Example:**  
1 → 2 → 3 → 4 → 5, k=2  
Output: 2 → 1 → 4 → 3 → 5

**Dart Code:**
ListNode? reverseKGroup(ListNode? head, int k) {
ListNode? curr = head;
int count = 0;

      while (curr != null && count < k) {
        curr = curr.next;
        count++;
      }

      if (count == k) {
        curr = reverseKGroup(curr, k);

        while (count-- > 0) {
          ListNode? temp = head!.next;
          head.next = curr;
          curr = head;
          head = temp;
        }

        head = curr;
      }

      return head;
    }

---

# 🎯 Key Patterns

- Reverse → Iterative pointer
- Fast & Slow → Cycle detection
- Dummy Node → Merge / Remove
- Two Pointer → Intersection
- Recursion → k-group reverse

---