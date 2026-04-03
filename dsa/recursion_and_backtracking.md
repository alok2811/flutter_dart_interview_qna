# 📌 Recursion & Backtracking (Top 7 Questions - Dart)

---

## 1. Combination Sum (LeetCode 39)

**Problem:**  
Find all combinations where numbers sum to target (reuse allowed).

**Example:**  
Input: candidates = [2,3,6,7], target = 7  
Output: [[2,2,3],[7]]

**Dart Code:**
List<List<int>> combinationSum(List<int> candidates, int target) {
List<List<int>> result = [];

      void backtrack(int start, int sum, List<int> path) {
        if (sum == target) {
          result.add(List.from(path));
          return;
        }

        if (sum > target) return;

        for (int i = start; i < candidates.length; i++) {
          path.add(candidates[i]);
          backtrack(i, sum + candidates[i], path);
          path.removeLast();
        }
      }

      backtrack(0, 0, []);
      return result;
    }

---

## 2. Permutations (LeetCode 46)

**Problem:**  
Return all possible permutations.

**Example:**  
[1,2,3] → [[1,2,3],[1,3,2],[2,1,3]...]

**Dart Code:**
List<List<int>> permute(List<int> nums) {
List<List<int>> result = [];

      void backtrack(List<int> path, List<bool> used) {
        if (path.length == nums.length) {
          result.add(List.from(path));
          return;
        }

        for (int i = 0; i < nums.length; i++) {
          if (used[i]) continue;

          used[i] = true;
          path.add(nums[i]);

          backtrack(path, used);

          path.removeLast();
          used[i] = false;
        }
      }

      backtrack([], List.filled(nums.length, false));
      return result;
    }

---

## 3. Subsets (LeetCode 78)

**Problem:**  
Return all possible subsets.

**Example:**  
[1,2] → [[],[1],[2],[1,2]]

**Dart Code:**
List<List<int>> subsets(List<int> nums) {
List<List<int>> result = [];

      void backtrack(int start, List<int> path) {
        result.add(List.from(path));

        for (int i = start; i < nums.length; i++) {
          path.add(nums[i]);
          backtrack(i + 1, path);
          path.removeLast();
        }
      }

      backtrack(0, []);
      return result;
    }

---

## 4. N-Queens (LeetCode 51)

**Problem:**  
Place N queens so that no two queens attack each other.

**Example:**  
n = 4 → 2 solutions

**Dart Code:**
List<List<String>> solveNQueens(int n) {
List<List<String>> result = [];
List<String> board =
List.generate(n, (_) => '.' * n);

      Set<int> cols = {};
      Set<int> diag1 = {};
      Set<int> diag2 = {};

      void backtrack(int row) {
        if (row == n) {
          result.add(List.from(board));
          return;
        }

        for (int col = 0; col < n; col++) {
          if (cols.contains(col) ||
              diag1.contains(row - col) ||
              diag2.contains(row + col)) continue;

          cols.add(col);
          diag1.add(row - col);
          diag2.add(row + col);

          board[row] =
              board[row].substring(0, col) +
              'Q' +
              board[row].substring(col + 1);

          backtrack(row + 1);

          cols.remove(col);
          diag1.remove(row - col);
          diag2.remove(row + col);

          board[row] =
              board[row].substring(0, col) +
              '.' +
              board[row].substring(col + 1);
        }
      }

      backtrack(0);
      return result;
    }

---

## 5. Letter Combinations of Phone Number (LeetCode 17)

**Problem:**  
Return all letter combinations for given digits.

**Example:**  
"23" → ["ad","ae","af","bd","be","bf","cd","ce","cf"]

**Dart Code:**
List<String> letterCombinations(String digits) {
if (digits.isEmpty) return [];

      Map<String, String> phone = {
        '2': 'abc',
        '3': 'def',
        '4': 'ghi',
        '5': 'jkl',
        '6': 'mno',
        '7': 'pqrs',
        '8': 'tuv',
        '9': 'wxyz'
      };

      List<String> result = [];

      void backtrack(int index, String path) {
        if (path.length == digits.length) {
          result.add(path);
          return;
        }

        String letters = phone[digits[index]]!;

        for (int i = 0; i < letters.length; i++) {
          backtrack(index + 1, path + letters[i]);
        }
      }

      backtrack(0, "");
      return result;
    }

---

## 6. Subsets II (LeetCode 90)

**Problem:**  
Return all subsets (no duplicates).

**Example:**  
[1,2,2] → [[],[1],[2],[1,2],[2,2],[1,2,2]]

**Dart Code:**
List<List<int>> subsetsWithDup(List<int> nums) {
nums.sort();
List<List<int>> result = [];

      void backtrack(int start, List<int> path) {
        result.add(List.from(path));

        for (int i = start; i < nums.length; i++) {
          if (i > start && nums[i] == nums[i - 1]) continue;

          path.add(nums[i]);
          backtrack(i + 1, path);
          path.removeLast();
        }
      }

      backtrack(0, []);
      return result;
    }

---

## 7. Sudoku Solver (LeetCode 37)

**Problem:**  
Fill the board so that every row, column, and box is valid.

**Dart Code:**
void solveSudoku(List<List<String>> board) {
void backtrack() {
for (int i = 0; i < 9; i++) {
for (int j = 0; j < 9; j++) {
if (board[i][j] == '.') {
for (int c = 1; c <= 9; c++) {
if (isValid(board, i, j, c.toString())) {
board[i][j] = c.toString();

                  backtrack();

                  board[i][j] = '.';
                }
              }
              return;
            }
          }
        }
      }

      backtrack();
    }

    bool isValid(List<List<String>> board, int row, int col, String val) {
      for (int i = 0; i < 9; i++) {
        if (board[row][i] == val) return false;
        if (board[i][col] == val) return false;

        int boxRow = 3 * (row ~/ 3) + i ~/ 3;
        int boxCol = 3 * (col ~/ 3) + i % 3;

        if (board[boxRow][boxCol] == val) return false;
      }
      return true;
    }

---

# 🎯 Key Patterns

- Backtracking → try → recurse → undo
- Path building → subsets / permutations
- Decision tree → include / exclude
- Pruning → skip duplicates
- Constraint checking → N-Queens / Sudoku

---