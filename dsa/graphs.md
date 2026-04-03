# 📌 Graphs (Top 6 Questions - Dart)

---

## 1. Clone Graph (LeetCode 133)

**Problem:**  
Given a reference of a node in a connected undirected graph, return a deep copy of the graph.

**Example:**  
Input: [[2,4],[1,3],[2,4],[1,3]]  
Output: Cloned graph with same structure

**Definition:**
class Node {
int val;
List<Node?> neighbors;

      Node(this.val, [List<Node?>? neighbors])
          : neighbors = neighbors ?? [];
    }

**Dart Code:**
Node? cloneGraph(Node? node) {
if (node == null) return null;

      Map<Node, Node> map = {};

      Node dfs(Node current) {
        if (map.containsKey(current)) {
          return map[current]!;
        }

        Node clone = Node(current.val);
        map[current] = clone;

        for (Node? neighbor in current.neighbors) {
          if (neighbor != null) {
            clone.neighbors.add(dfs(neighbor));
          }
        }

        return clone;
      }

      return dfs(node);
    }

**Approach:**  
Use DFS + HashMap.  
If a node is already cloned, reuse it. Otherwise create clone and recursively clone neighbors.

**Time Complexity:** O(V + E)  
**Space Complexity:** O(V)

---

## 2. Number of Islands (LeetCode 200)

**Problem:**  
Count the number of islands in a 2D grid.  
An island is formed by connected `'1'` cells.

**Example:**  
Input:  
[
["1","1","0","0","0"],
["1","1","0","0","0"],
["0","0","1","0","0"],
["0","0","0","1","1"]
]  
Output: 3

**Dart Code:**
int numIslands(List<List<String>> grid) {
int rows = grid.length;
int cols = grid[0].length;
int count = 0;

      void dfs(int r, int c) {
        if (r < 0 ||
            c < 0 ||
            r >= rows ||
            c >= cols ||
            grid[r][c] == '0') {
          return;
        }

        grid[r][c] = '0';

        dfs(r + 1, c);
        dfs(r - 1, c);
        dfs(r, c + 1);
        dfs(r, c - 1);
      }

      for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
          if (grid[i][j] == '1') {
            count++;
            dfs(i, j);
          }
        }
      }

      return count;
    }

**Approach:**  
When you find land, start DFS and mark the whole island as visited.

**Time Complexity:** O(m × n)  
**Space Complexity:** O(m × n) in worst case recursion stack

---

## 3. Course Schedule (LeetCode 207)

**Problem:**  
There are `numCourses` courses and prerequisites.  
Return `true` if you can finish all courses.

**Example:**  
Input: numCourses = 2, prerequisites = [[1,0]]  
Output: true

**Dart Code:**
bool canFinish(int numCourses, List<List<int>> prerequisites) {
List<List<int>> graph =
List.generate(numCourses, (_) => []);
List<int> indegree = List.filled(numCourses, 0);

      for (var pair in prerequisites) {
        int course = pair[0];
        int prereq = pair[1];
        graph[prereq].add(course);
        indegree[course]++;
      }

      List<int> queue = [];
      for (int i = 0; i < numCourses; i++) {
        if (indegree[i] == 0) {
          queue.add(i);
        }
      }

      int completed = 0;
      int index = 0;

      while (index < queue.length) {
        int current = queue[index++];
        completed++;

        for (int neighbor in graph[current]) {
          indegree[neighbor]--;
          if (indegree[neighbor] == 0) {
            queue.add(neighbor);
          }
        }
      }

      return completed == numCourses;
    }

**Approach:**  
Use topological sort (Kahn’s Algorithm).  
If all courses can be processed, no cycle exists.

**Time Complexity:** O(V + E)  
**Space Complexity:** O(V + E)

---

## 4. Is Graph Bipartite? (LeetCode 785)

**Problem:**  
Check if a graph can be colored using 2 colors such that no adjacent nodes have same color.

**Example:**  
Input: [[1,3],[0,2],[1,3],[0,2]]  
Output: true

**Dart Code:**
bool isBipartite(List<List<int>> graph) {
int n = graph.length;
List<int> color = List.filled(n, 0);

      for (int i = 0; i < n; i++) {
        if (color[i] != 0) continue;

        List<int> queue = [i];
        color[i] = 1;
        int index = 0;

        while (index < queue.length) {
          int node = queue[index++];

          for (int neighbor in graph[node]) {
            if (color[neighbor] == 0) {
              color[neighbor] = -color[node];
              queue.add(neighbor);
            } else if (color[neighbor] == color[node]) {
              return false;
            }
          }
        }
      }

      return true;
    }

**Approach:**  
Use BFS coloring.  
If a neighbor gets same color as current node, graph is not bipartite.

**Time Complexity:** O(V + E)  
**Space Complexity:** O(V)

---

## 5. Rotting Oranges (LeetCode 994)

**Problem:**  
Every minute, rotten oranges make adjacent fresh oranges rotten.  
Return minimum minutes to rot all oranges, or -1 if impossible.

**Example:**  
Input: [[2,1,1],[1,1,0],[0,1,1]]  
Output: 4

**Dart Code:**
int orangesRotting(List<List<int>> grid) {
int rows = grid.length;
int cols = grid[0].length;

      List<List<int>> queue = [];
      int fresh = 0;

      for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
          if (grid[i][j] == 2) {
            queue.add([i, j]);
          } else if (grid[i][j] == 1) {
            fresh++;
          }
        }
      }

      int minutes = 0;
      int index = 0;
      List<List<int>> directions = [
        [1, 0],
        [-1, 0],
        [0, 1],
        [0, -1]
      ];

      while (index < queue.length && fresh > 0) {
        int size = queue.length - index;

        for (int i = 0; i < size; i++) {
          List<int> cell = queue[index++];
          int r = cell[0];
          int c = cell[1];

          for (var dir in directions) {
            int nr = r + dir[0];
            int nc = c + dir[1];

            if (nr >= 0 &&
                nc >= 0 &&
                nr < rows &&
                nc < cols &&
                grid[nr][nc] == 1) {
              grid[nr][nc] = 2;
              fresh--;
              queue.add([nr, nc]);
            }
          }
        }

        minutes++;
      }

      return fresh == 0 ? minutes : -1;
    }

**Approach:**  
Use multi-source BFS starting from all rotten oranges at once.

**Time Complexity:** O(m × n)  
**Space Complexity:** O(m × n)

---

## 6. Number of Connected Components in an Undirected Graph (LeetCode 323)

**Problem:**  
Given `n` nodes and edges, return the number of connected components.

**Example:**  
Input: n = 5, edges = [[0,1],[1,2],[3,4]]  
Output: 2

**Dart Code:**
int countComponents(int n, List<List<int>> edges) {
List<List<int>> graph = List.generate(n, (_) => []);
List<bool> visited = List.filled(n, false);

      for (var edge in edges) {
        int u = edge[0];
        int v = edge[1];
        graph[u].add(v);
        graph[v].add(u);
      }

      void dfs(int node) {
        visited[node] = true;

        for (int neighbor in graph[node]) {
          if (!visited[neighbor]) {
            dfs(neighbor);
          }
        }
      }

      int count = 0;

      for (int i = 0; i < n; i++) {
        if (!visited[i]) {
          count++;
          dfs(i);
        }
      }

      return count;
    }

**Approach:**  
Build adjacency list.  
Run DFS from every unvisited node. Each DFS marks one connected component.

**Time Complexity:** O(V + E)  
**Space Complexity:** O(V + E)

---

# 🎯 Key Patterns

- DFS + HashMap → Clone Graph
- Grid DFS → Number of Islands
- Topological Sort → Course Schedule
- BFS / Coloring → Bipartite Graph
- Multi-source BFS → Rotting Oranges
- DFS / Components → Connected Components

---