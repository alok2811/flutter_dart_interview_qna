# 📌 Trees (Top 8 Questions - Dart)

---

## Definition

    class TreeNode {
      int val;
      TreeNode? left;
      TreeNode? right;

      TreeNode(this.val, [this.left, this.right]);
    }

---

## 1. Maximum Depth of Binary Tree (LeetCode 104)

**Problem:**  
Find the maximum depth of a binary tree.

**Example:**  
Input: root = [3,9,20,null,null,15,7]  
Output: 3

**Dart Code:**
int maxDepth(TreeNode? root) {
if (root == null) return 0;

      int leftDepth = maxDepth(root.left);
      int rightDepth = maxDepth(root.right);

      return 1 + (leftDepth > rightDepth ? leftDepth : rightDepth);
    }

**Approach:**  
Use recursion and return 1 + maximum depth of left and right subtree.

**Time Complexity:** O(n)

---

## 2. Same Tree (LeetCode 100)

**Problem:**  
Check if two binary trees are exactly the same.

**Example:**  
Input: p = [1,2,3], q = [1,2,3]  
Output: true

**Dart Code:**
bool isSameTree(TreeNode? p, TreeNode? q) {
if (p == null && q == null) return true;
if (p == null || q == null) return false;
if (p.val != q.val) return false;

      return isSameTree(p.left, q.left) &&
             isSameTree(p.right, q.right);
    }

**Approach:**  
Compare current nodes, then recursively compare left and right subtree.

**Time Complexity:** O(n)

---

## 3. Symmetric Tree (LeetCode 101)

**Problem:**  
Check whether a binary tree is symmetric around its center.

**Example:**  
Input: root = [1,2,2,3,4,4,3]  
Output: true

**Dart Code:**
bool isSymmetric(TreeNode? root) {
return isMirror(root?.left, root?.right);
}

    bool isMirror(TreeNode? left, TreeNode? right) {
      if (left == null && right == null) return true;
      if (left == null || right == null) return false;
      if (left.val != right.val) return false;

      return isMirror(left.left, right.right) &&
             isMirror(left.right, right.left);
    }

**Approach:**  
Compare left subtree of one side with right subtree of the other side.

**Time Complexity:** O(n)

---

## 4. Binary Tree Preorder Traversal (LeetCode 144)

**Problem:**  
Return preorder traversal of a binary tree.

**Order:** Root → Left → Right

**Example:**  
Input: root = [1,null,2,3]  
Output: [1,2,3]

**Dart Code:**
List<int> preorderTraversal(TreeNode? root) {
List<int> result = [];

      void dfs(TreeNode? node) {
        if (node == null) return;

        result.add(node.val);
        dfs(node.left);
        dfs(node.right);
      }

      dfs(root);
      return result;
    }

**Approach:**  
Visit root first, then left subtree, then right subtree.

**Time Complexity:** O(n)

---

## 5. Binary Tree Inorder Traversal (LeetCode 94)

**Problem:**  
Return inorder traversal of a binary tree.

**Order:** Left → Root → Right

**Example:**  
Input: root = [1,null,2,3]  
Output: [1,3,2]

**Dart Code:**
List<int> inorderTraversal(TreeNode? root) {
List<int> result = [];

      void dfs(TreeNode? node) {
        if (node == null) return;

        dfs(node.left);
        result.add(node.val);
        dfs(node.right);
      }

      dfs(root);
      return result;
    }

**Approach:**  
Visit left subtree first, then root, then right subtree.

**Time Complexity:** O(n)

---

## 6. Binary Tree Postorder Traversal (LeetCode 145)

**Problem:**  
Return postorder traversal of a binary tree.

**Order:** Left → Right → Root

**Example:**  
Input: root = [1,null,2,3]  
Output: [3,2,1]

**Dart Code:**
List<int> postorderTraversal(TreeNode? root) {
List<int> result = [];

      void dfs(TreeNode? node) {
        if (node == null) return;

        dfs(node.left);
        dfs(node.right);
        result.add(node.val);
      }

      dfs(root);
      return result;
    }

**Approach:**  
Visit left subtree, then right subtree, then root.

**Time Complexity:** O(n)

---

## 7. Binary Tree Level Order Traversal (LeetCode 102)

**Problem:**  
Return the level order traversal of a binary tree.

**Example:**  
Input: root = [3,9,20,null,null,15,7]  
Output: [[3],[9,20],[15,7]]

**Dart Code:**
List<List<int>> levelOrder(TreeNode? root) {
if (root == null) return [];

      List<List<int>> result = [];
      List<TreeNode> queue = [root];

      while (queue.isNotEmpty) {
        int size = queue.length;
        List<int> level = [];

        for (int i = 0; i < size; i++) {
          TreeNode node = queue.removeAt(0);
          level.add(node.val);

          if (node.left != null) queue.add(node.left!);
          if (node.right != null) queue.add(node.right!);
        }

        result.add(level);
      }

      return result;
    }

**Approach:**  
Use BFS with a queue and process one level at a time.

**Time Complexity:** O(n)

---

## 8. Balanced Binary Tree (LeetCode 110)

**Problem:**  
Check if the binary tree is height-balanced.

**Example:**  
Input: root = [3,9,20,null,null,15,7]  
Output: true

**Dart Code:**
bool isBalanced(TreeNode? root) {
return height(root) != -1;
}

    int height(TreeNode? node) {
      if (node == null) return 0;

      int left = height(node.left);
      if (left == -1) return -1;

      int right = height(node.right);
      if (right == -1) return -1;

      if ((left - right).abs() > 1) return -1;

      return 1 + (left > right ? left : right);
    }

**Approach:**  
Return tree height recursively.  
If any subtree is unbalanced, return -1.

**Time Complexity:** O(n)

---

# 🎯 Key Patterns

- DFS recursion → depth / traversals / compare trees
- Mirror recursion → symmetric tree
- BFS queue → level order traversal
- Bottom-up height check → balanced tree

---