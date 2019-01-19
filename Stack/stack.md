## 155[Min Stack](https://leetcode.com/problems/min-stack)    

```java
class MinStack {
    Stack<Integer> stack;
    int min;
    /** initialize your data structure here. */
    public MinStack() {
        stack = new Stack();
        min = Integer.MAX_VALUE;
    }
    
    public void push(int x) {
        if (x <= min) {
            stack.push(min);
            min = x;
        }
        stack.push(x);
    }
    
    public void pop() {
        if (stack.pop() == min) {
            min = stack.pop();
        }
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return min;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */



// class MinStack {
//     Stack<Long> stack;
//     //int min => wrong ?????? cast problem??????
//     long min;
//     /** initialize your data structure here. */
//     public MinStack() {
//         stack = new Stack();
//         min = Long.MAX_VALUE;
//     }
    
//     public void push(int x) {
//         // if (stack.isEmpty()) {
//         //     stack.push(0L);
//         //     min = x;
//         // }
//         // else {
//         //     stack.push(x - min);
//         //     if (min > x) {
//         //         min = x;
//         //     }
//         // }
        
//         if (stack.isEmpty()) {
//             min = x;
//         }
//         stack.push(x - min);
//         if (min > x) {
//             min = x;
//         }
//     }
    
//     public void pop() {
//         if (stack.isEmpty()) {
//             return;
//         }
//         long top = stack.pop();
//         if (top < 0) {
//             min -= top;
//         }
//     }
    
//     public int top() {
//         long top = stack.peek();
//         return top <= 0 ? (int) min : (int) (min + top);
//     }
    
//     public int getMin() {
//         return (int) min;
//     }
// }

// /**
//  * Your MinStack object will be instantiated and called as such:
//  * MinStack obj = new MinStack();
//  * obj.push(x);
//  * obj.pop();
//  * int param_3 = obj.top();
//  * int param_4 = obj.getMin();
//  */


// class MinStack {
//     Stack<Long> stack;
//     //int min => wrong ?????? cast problem??????
//     int min;
//     /** initialize your data structure here. */
//     public MinStack() {
//         stack = new Stack();
//     }
    
//     public void push(int x) {
//         // if (stack.isEmpty()) {
//         //     stack.push(0L);
//         //     min = x;
//         // }
//         // else {
//         //     stack.push(x - min);
//         //     if (min > x) {
//         //         min = x;
//         //     }
//         // }
        
//         if (stack.isEmpty()) {
//             min = x;
//         }
//         stack.push((long)x - min); //solve cast problem
//         if (min > x) {
//             min = x;
//         }
//     }
    
//     public void pop() {
//         if (stack.isEmpty()) {
//             return;
//         }
//         long top = stack.pop();
//         if (top < 0) {
//             min = (int)((long)min - top); //solve cast problem
//         }
//     }
    
//     public int top() {
//         long top = stack.peek();
//         return top <= 0 ? min : (int) ((long)min + top); //solve cast problem
//     }
    
//     public int getMin() {
//         return min;
//     }
// }

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */


```







## 20[Valid Parentheses](https://leetcode.com/problems/valid-parentheses)  

```java
// class Solution {
//     public boolean isValid(String s) {
//         Stack<Character> stack = new Stack();
//         // for (int i = 0; i < s.length(); i++) {
//         //     char c = s.charAt(i);
        
//         for (char c : s.toCharArray()) {
//             if (c == '(') {
//                 stack.push(')');
//             }
//             else if (c == '{') {
//                 stack.push('}');
//             }
//             else if (c == '[') {
//                 stack.push(']');
//             }
//             else if (stack.isEmpty() || stack.pop() != c){
//                 return false;
//             }
//         }
//         return stack.isEmpty();
//     }
// }


// class Solution {
//     public boolean isValid(String s) {
//         Stack<Character> stack = new Stack();
//         // for (int i = 0; i < s.length(); i++) {
//         //     char c = s.charAt(i);
        
//         for (char c : s.toCharArray()) {
//             if (c == '(' || c == '{' || c == '[') {
//                 stack.push(c);
//             }
//             else if (c == ')' && !stack.isEmpty() && stack.peek() == '(') {
//                 stack.pop();
//             }
//             else if (c == '}' && !stack.isEmpty() && stack.peek() == '{') {
//                 stack.pop();
//             }
//             else if (c == ']' && !stack.isEmpty() && stack.peek() == '[') {
//                 stack.pop();
//             }
//             else {
//                 return false;
//             }
//         }
//         return stack.isEmpty();
//     }
// }


// class Solution {
//     public boolean isValid(String s) {
//         Stack<Character> stack = new Stack();
//         // for (int i = 0; i < s.length(); i++) {
//         //     char c = s.charAt(i);
//         Map<Character, Character> map = new HashMap();
//         map.put('(',')');
//         map.put('{','}');
//         map.put('[',']');
        
//         for (char c : s.toCharArray()) {
//             if (map.containsKey(c)) {
//                 stack.push(map.get(c));
//             } else {
//                 char top = stack.isEmpty() ? '#' : stack.pop();
//                 if (top != c) {
//                     return false;
//                 } 
//             }
//         }
//         return stack.isEmpty();
//     }
// }


class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack();
        // for (int i = 0; i < s.length(); i++) {
        //     char c = s.charAt(i);
        Map<Character, Character> map = new HashMap();
        map.put(')','(');
        map.put('}','{');
        map.put(']','[');
        
        for (char c : s.toCharArray()) {
            if (!map.containsKey(c)) {
                stack.push(c);
            } else {
                char top = stack.isEmpty() ? '#' : stack.pop();
                if (top != map.get(c)) {
                    return false;
                } 
            }
        }
        return stack.isEmpty();
    }
}
```







## 739[Daily Temperatures](https://leetcode.com/problems/daily-temperatures)  

```java
// class Solution {
//     public int[] dailyTemperatures(int[] T) {
//         int[] res = new int[T.length];
//         for (int i = 0; i < T.length; i++) {
//             for (int j = i + 1; j < T.length; j++) {
//                 if (T[j] > T[i]) {
//                     res[i] = j - i;
//                     break;
//                 }
//             }
//         }
//         return res;
//     }
// }


// class Solution {
//     public int[] dailyTemperatures(int[] T) {
//         int[] ans = new int[T.length];
        
//         //T: [30, 100]
//         int[] next = new int[101];
//         Arrays.fill(next, Integer.MAX_VALUE);
        
//         //reverse order to make sure next[T[i]] = i; i is always the smallest one for T[i]
//         for (int i = T.length - 1; i >=0; i--) {
//             int warmer_index = Integer.MAX_VALUE;
            
//             //update the valid nearest warm_index from T[i] _ 1 to 100
//             for (int j = T[i] + 1; j <= 100; j++) {
//                 if (next[j] < warmer_index) {
//                     warmer_index = next[j];
//                 }
//             }
            
//             //update the distance between valid warmer_index and i to ans
//             if (warmer_index != Integer.MAX_VALUE) {
//                 ans[i] = warmer_index - i;
//             }
            
//             //update T T[i] => i
//             next[T[i]] = i;
            
//         }
//         return ans;
//     }
// }


// class Solution {
//     public int[] dailyTemperatures(int[] T) {
//         if (T == null) {
//             return null;
//         }
        
//         Stack<Integer> stack = new Stack();
//         int[] res = new int[T.length];
        
//         //reverse 
//         for (int i = T.length - 1; i >= 0; i--) { 
//             // make sure values in stack are all larger than T[i]
//             while (!stack.isEmpty() && T[i] >= T[stack.peek()]) {
//                 stack.pop();
//             }
                // no empty means there is some value larger than i
//             if (!stack.isEmpty()) {
//                 res[i] = stack.peek() - i;
//             }
//             else {
//                 res[i] = 0;
//             }
//             stack.push(i);
//         }
        
//         return res;
//     }
// }



class Solution {
    public int[] dailyTemperatures(int[] T) {
        if (T == null) {
            return null;
        }
        
        Stack<Integer> stack = new Stack();
        int[] res = new int[T.length];
        
        for (int i = 0; i < T.length; i++) { 
            // make sure values in stack smaller than T[i] poped can get the value
            while (!stack.isEmpty() && T[i] > T[stack.peek()]) {
                int idx = stack.pop();
                res[idx] = i - idx;
            }
            stack.push(i);
        }
        
        return res;
    }
}


// class Solution {
//     public int[] dailyTemperatures(int[] T) {
//         if (T == null) {
//             return null;
//         }
        
//         int top = -1;
//         int[] stack = new int[T.length];
//         int[] res = new int[T.length];
        
     
//         for (int i = 0; i < T.length; i++) { 
//             //while (!stack.isEmpty() && T[i] > T[stack.peek()]) {
//             while (top != -1 && T[i] > T[stack[top]]) {
//                 //int idx = stack.pop();
//                 int idx = stack[top--];
//                 res[idx] = i - idx;
//             }
//             //stack.push(i);
//             stack[++top] = i;
//         }
        
//         return res;
//     }
// }
```





## 150[Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation)  

```java
class Solution {
    public int evalRPN(String[] tokens) {
        // Set<String> set = new HashSet();
        // set.add("+");
        // set.add("-");
        // set.add("*");
        // set.add("/");
        
        Stack<Integer> stack = new Stack();
        for (String element : tokens) {
            if (element.equals("+")) {
                int right = stack.pop();
                int left = stack.pop();
         
                stack.push(left + right);
            }
            else if (element.equals("-")) {
                int right = stack.pop();
                int left = stack.pop();
      
                stack.push(left - right);
            }
            else if (element.equals("*")) {
                int right = stack.pop();
                int left = stack.pop();
         
                stack.push(left * right);
            }
            else if (element.equals("/")) {
                int right = stack.pop();
                int left = stack.pop();
      
                stack.push(left / right);
            }
            else {
                stack.push(Integer.valueOf(element));
            }
        }

        return stack.pop();
      
    }
}


// class Solution {
//     public int evalRPN(String[] tokens) {
//         Set<String> set = new HashSet();
//         set.add("+");
//         set.add("-");
//         set.add("*");
//         set.add("/");
        
//         Stack<String> stack = new Stack();
//         for (String element : tokens) {
//             if (set.contains(element)) {
//                 String right = stack.pop();
//                 String left = stack.pop();
//                 // how to use eval?
//                 stack.push(eval(left + element + right));
//             }
//             else {
//                 stack.push(element);
//             }
//         }

//         return stack.pop();
      
//     }
// }
```





## 200[Number of Islands](https://leetcode.com/problems/number-of-islands)   

```java
// class Solution {
//     public int numIslands(char[][] grid) {
//         if (grid == null) {
//             return 0;
//         }
//         int count = 0;
//         for (int i = 0; i < grid.length; i++) {
//             for (int j = 0; j < grid[0].length; j++) {
//                 if (grid[i][j] == '1') {
//                     count++;
//                     bfs(grid, i, j);
//                 }
//             }
//         }
//         return count;
//     }

    
//     private void bfs(char[][] grid, int i, int j) {
//         grid[i][j] = '0';
//         Queue<Integer> queue = new LinkedList();
//         int nr = grid.length;
//         int nc = grid[0].length;
//         int code = i * nc + j;
//         queue.offer(code);
        
//         while (!queue.isEmpty()) {
//             int currCode = queue.poll();
            
//             int r = currCode / nc;
//             int c = currCode % nc;
            
//             //up
//             if (r - 1 >= 0 && grid[r - 1][c] == '1') {
//                 grid[r - 1][c] = '0';
//                 queue.offer((r-1) * nc + c);
//             }
//             //down
//             if (r + 1 < nr && grid[r + 1][c] == '1') {
//                 grid[r + 1][c] = '0';
//                 queue.offer((r+1) * nc + c);
//             }
//             //left
//             if (c - 1 >= 0 && grid[r][c - 1] == '1') {
//                 grid[r][c - 1] = '0';
//                 queue.offer(r * nc + c - 1);
//             }
//             //right
//             if (c + 1 < nc && grid[r][c + 1] == '1') {
//                 grid[r][c + 1] = '0';
//                 queue.offer(r * nc + c + 1);
//             }
//         }
//     }
// }


// class Solution { 
//     public int numIslands(char[][] grid) {
//         if (grid == null) {
//             return 0;
//         }
//         int count = 0;
//         for (int i = 0; i < grid.length; i++) {
//             for (int j = 0; j < grid[0].length; j++) {
//                 if (grid[i][j] == '1') {
//                     count++;
//                     bfs(grid, i, j);
//                 }
//             }
//         }
//         return count;
//     }

    
//     private void bfs(char[][] grid, int i, int j) {
//         grid[i][j] = '0';
//         int[] deltaX = {-1, 1, 0, 0};
//         int[] deltaY = {0, 0, -1, 1};
//         Queue<Integer> queue = new LinkedList();
//         int nr = grid.length;
//         int nc = grid[0].length;
//         int code = i * nc + j;
//         queue.offer(code);
        
//         while (!queue.isEmpty()) {
//             Integer currCode = queue.poll();
            
//             int r = currCode / nc;
//             int c = currCode % nc;
            
//             for (int k = 0; k < 4; k++) {
//                 int newR = r + deltaX[k];
//                 int newC = c + deltaY[k];
                
//                 if (newR < 0 || newR >= nr || newC < 0 || newC >= nc)  {
//                     continue;
//                 }
                
//                 //System.out.println("newR" + newR + " newC" + newC);
//                 if (grid[newR][newC] == '1') {
//                     grid[newR][newC] = '0';
//                     queue.offer(newR * nc + newC);
//                 }
//             }
//         }
//     }
// }



class Solution { 
    private final int[] deltaX = {-1, 1, 0, 0};
    private final int[] deltaY = {0, 0, -1, 1};
    
    public int numIslands(char[][] grid) {
        if (grid == null) {
            return 0;
        }
        int count = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '1') {
                    count++;
                    dfs(grid, i, j);
                }
            }
        }
        return count;
    }

// tail recursion
    private void dfs(char[][] grid, int i, int j) {
        if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] == '0')  {
            return;
        }        
        grid[i][j] = '0';
        for (int k = 0; k < 4; k++) {
            int newR = i + deltaX[k];
            int newC = j + deltaY[k];

            // if (newR < 0 || newR >= grid.length || newC < 0 || newC >= grid[0].length || grid[newR][newC] == '0')  {
            //     continue;
            // }
            dfs(grid, newR, newC);
        }
    }
    
    
//Linear Recursive
    // private void dfs(char[][] grid, int i, int j) {
    //     if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] == '0') {
    //         return;
    //     }
    //     grid[i][j] = '0';
    //     for (int k = 0; k < 4; k++) {
    //         int newR = i + deltaX[k];
    //         int newC = j + deltaY[k];
    //         dfs(grid, newR, newC);
    //     }
    // }
}



// class Solution {
//     private class Coordinate {
//         int x;
//         int y;
//         Coordinate(int x, int y) {
//             this.x = x;
//             this.y = y;
//         }
//     }
    
//     public int numIslands(char[][] grid) {
//         if (grid == null) {
//             return 0;
//         }
//         int count = 0;
//         for (int i = 0; i < grid.length; i++) {
//             for (int j = 0; j < grid[0].length; j++) {
//                 if (grid[i][j] == '1') {
//                     count++;
//                     bfs(grid, i, j);
//                 }
//             }
//         }
//         return count;
//     }

    
//     private void bfs(char[][] grid, int i, int j) {
//         grid[i][j] = '0';
//         int[] deltaX = {-1, 1, 0, 0};
//         int[] deltaY = {0, 0, -1, 1};
//         Queue<Coordinate> queue = new LinkedList();
//         int nr = grid.length;
//         int nc = grid[0].length;
//         //System.out.println("nr" + nr + " nc" + nc);
//         queue.offer(new Coordinate(i, j));
        
//         while (!queue.isEmpty()) {
//             Coordinate coordinate = queue.poll();
            
//             int r = coordinate.x;
//             int c = coordinate.y;
            
//             for (int k = 0; k < 4; k++) {
//                 int newR = r + deltaX[k];
//                 int newC = c + deltaY[k];
                
//                 if (newR < 0 || newR >= nr || newC < 0 || newC >= nc)  {
//                     continue;
//                 }
                
//                 //System.out.println("newR" + newR + " newC" + newC);
//                 if (grid[newR][newC] == '1') {
//                     grid[newR][newC] = '0';
//                     queue.offer(new Coordinate(newR, newC));
//                 }
//             }
//         }
//     }
// }
```



## 133[Clone Graph](https://leetcode.com/problems/clone-graph)    

```java
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     List<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    Map<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap();
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if (node == null) {
            return null;
        }
        if (map.containsKey(node)) { //class UndirectedGraphNode  hashCode , equals??????? 
            return map.get(node);
        }
        UndirectedGraphNode copy = new UndirectedGraphNode(node.label);
        map.put(node, copy);
        for (UndirectedGraphNode neighbor : node.neighbors) {
            copy.neighbors.add(cloneGraph(neighbor));
        }
        return copy;
    }
}


// public class Solution {
//     Map<Integer, UndirectedGraphNode> map = new HashMap();
//     public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
//         if (node == null) {
//             return null;
//         }
//         if (map.containsKey(node.label)) {
//             return map.get(node.label);
//         }
//         UndirectedGraphNode copy = new UndirectedGraphNode(node.label);
//         map.put(node.label, copy);
//         for (UndirectedGraphNode neighbor : node.neighbors) {
//             copy.neighbors.add(cloneGraph(neighbor));
//         }
//         return copy;
//     }
// }



// public class Solution {
//     public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
//         if (node == null) {
//             return null;
//         }
//         Map<Integer, UndirectedGraphNode> map = new HashMap();
//         UndirectedGraphNode copyHead = new UndirectedGraphNode(node.label);
//         map.put(node.label, copyHead);
//         Queue<UndirectedGraphNode> queue = new LinkedList();
//         queue.offer(node);
//         while (!queue.isEmpty()) {
//             UndirectedGraphNode curr = queue.poll();
            
//             for (UndirectedGraphNode neighbor : curr.neighbors) {
//                 if (!map.containsKey(neighbor.label)) {
//                     map.put(neighbor.label, new UndirectedGraphNode(neighbor.label));
//                     queue.offer(neighbor);
//                 }
//                 map.get(curr.label).neighbors.add(map.get(neighbor.label));
//             }
//         }
//         return copyHead;
//     }
// }


// public class Solution {
//     public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
//         if (node == null) {
//             return null;
//         }
//         Map<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap();
//         UndirectedGraphNode copyHead = new UndirectedGraphNode(node.label);
//         map.put(node, copyHead);
//         Queue<UndirectedGraphNode> queue = new LinkedList();
//         queue.offer(node);
//         while (!queue.isEmpty()) {
//             UndirectedGraphNode curr = queue.poll();
            
//             for (UndirectedGraphNode neighbor : curr.neighbors) {
//                 if (!map.containsKey(neighbor)) {
//                     map.put(neighbor, new UndirectedGraphNode(neighbor.label));
//                     queue.offer(neighbor);
//                 }
//                 map.get(curr).neighbors.add(map.get(neighbor));
//             }
//         }
//         return copyHead;
//     }
// }
```









494 [Target Sum](https://leetcode.com/problems/target-sum)   

```java
class Solution {
    public int findTargetSumWays(int[] nums, int S) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int[][] memory = new int[nums.length][2001];
        for (int[] row: memory) {
            Arrays.fill(row, -1001);
        }
        return helper(nums, S, 0, 0, memory);
    }
    
    private int helper (int[] nums, int S, int sum, int index, int[][] memory) {
        if (index == nums.length) {
            return sum != S ? 0 : 1;
        }
        //System.out.println(memory[index][sum + 1000]);
        if (memory[index][sum + 1000] == -1001) {
            int add = helper(nums, S, sum + nums[index], index + 1, memory);
            int substract = helper(nums, S, sum - nums[index], index + 1, memory);
            memory[index][sum + 1000] = add + substract;
        }
        return memory[index][sum + 1000];
    }
}
```







## 94 [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal)   

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    //version 1
    public List<Integer> inorderTraversal(TreeNode root) {
        if (root == null) {
                return new ArrayList<Integer>();
        }            
        List<Integer> pre = inorderTraversal(root.left);
        pre.add(root.val);
        List<Integer> after = inorderTraversal(root.right);
        pre.addAll(after);
        return pre;
    }
    
    
//     //version 2
//     public List<Integer> inorderTraversal(TreeNode root) {
//         List<Integer> result = new ArrayList();
//         inorderTraversalHelper(root, result);
//         return result;
//     }
    
//     private void inorderTraversalHelper(TreeNode root, List<Integer> result) {
//         if (root == null) {
//             return;
//         }
//         inorderTraversalHelper(root.left, result);
//         result.add(root.val);
//         inorderTraversalHelper(root.right, result);
//     }
    
    //version 3 iterative 
    // public List<Integer> inorderTraversal(TreeNode root) {
    //     List<Integer> result = new ArrayList();
    //     Stack<TreeNode> stack = new Stack();
    //     if (root == null) {
    //         return result;
    //     }
    //     TreeNode currNode = root;
    //     while (currNode != null || !stack.isEmpty()) {
    //         while (currNode != null) {
    //             stack.push(currNode);
    //             currNode = currNode.left;
    //         }
    //         currNode = stack.pop();
    //         result.add(currNode.val);
    //         currNode = currNode.right;
    //     }
    //     return result;
    // }
    
    // //version 4
    // public List<Integer> inorderTraversal(TreeNode root) {
    //     List<Integer> result = new ArrayList();
    //     Stack<TreeNode> stack = new Stack();
    //     if (root == null) {
    //         return result;
    //     }
    //     TreeNode currNode = root;
    //     while (currNode != null || !stack.isEmpty()) {
    //         if (currNode != null) {
    //             stack.push(currNode);
    //             currNode = currNode.left;
    //         } else {
    //             currNode = stack.pop();
    //             result.add(currNode.val);
    //             currNode = currNode.right;
    //         }
    //     }
    //     return result;
    // }
    
    
//     public List<Integer> inorderTraversal(TreeNode root) {
//         if (root == null) {
//             return new ArrayList();
//         }
//         List<Integer> res = new ArrayList();
//         Stack<TreeNode> stack = new Stack();
   
//         // while (root != null || !stack.isEmpty()) {
//         //     if (root == null) { 
//         //         TreeNode curr = stack.pop();
//         //         res.add(curr.val);
//         //         root = curr.right;
//         //     }
//         //     else {
//         //         stack.push(root);
//         //         root = root.left;
//         //     }
//         // }
        
//         while (root != null || !stack.isEmpty()) {
//             while (root != null) {
//                 stack.push(root);
//                 root = root.left;
//             }
//             TreeNode curr = stack.pop();
//             res.add(curr.val);
//             root = curr.right;
//         }
        
//         return res;
//     }
}
```







## 232[Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks)  

```java
// class MyQueue {
//     Stack<Integer> stack;
//     Stack<Integer> stack2;
//     int front;
//     /** Initialize your data structure here. */
//     public MyQueue() {
//         stack = new Stack();
//         stack2 = new Stack();
//     }
    
//     /** Push element x to the back of queue. */
//     public void push(int x) {
//         if (stack.isEmpty()) {
//             front = x;
//         }
//         while (!stack.isEmpty()) {
//             stack2.push(stack.pop());
//         }
//         stack.push(x);
//         while (!stack2.isEmpty()) {
//             stack.push(stack2.pop());
//         }
//     }
    
//     /** Removes the element from in front of queue and returns that element. */
//     public int pop() {
//         int res = stack.pop();
//         if (!stack.isEmpty()){
//             front = stack.peek();
//         }
//         return res;
        
//     }
    
//     /** Get the front element. */
//     public int peek() {
//         //return stack.peek();
//         return front;
//     }
    
//     /** Returns whether the queue is empty. */
//     public boolean empty() {
//         return stack.isEmpty();
//     }
// }

// /**
//  * Your MyQueue object will be instantiated and called as such:
//  * MyQueue obj = new MyQueue();
//  * obj.push(x);
//  * int param_2 = obj.pop();
//  * int param_3 = obj.peek();
//  * boolean param_4 = obj.empty();
//  */


class MyQueue {
    Stack<Integer> stack;
    Stack<Integer> stack2;
    //front is the pointer for front of stack instead of stack2
    int front; 
    /** Initialize your data structure here. */
    public MyQueue() {
        stack = new Stack();
        stack2 = new Stack();
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        if (stack.isEmpty()) {
            front = x;
        }
        stack.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        if (stack2.isEmpty()){
            while (!stack.isEmpty()) {
                stack2.push(stack.pop());
            }
        }
        int res = stack2.pop();
        return res;
        
    }
    
    /** Get the front element. */
    public int peek() {
        //return stack.peek();
        if (!stack2.isEmpty()) {
            return stack2.peek();
        }
        //front is the pointer for front of stack, stack2.peek() is the front of stack2
        return front;
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return stack.isEmpty() && stack2.isEmpty();
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */



```





## 394 [Decode String](https://leetcode.com/problems/decode-string)   

```java
// class Solution {
//     public String decodeString(String s) {
//         Stack<Integer> count = new Stack();
//         Stack<String> stack = new Stack();
//         stack.push("");
//         int i = 0;
//         while (i < s.length()) {
//             char c = s.charAt(i);
//             if (c >= '0' && c <= '9') {
//                 int start = i;
                
//                 // int end = start + 1;
//                 // while (s.charAt(end) >= '0' && s.charAt(end) <= '9') {
//                 //     end++;
//                 // }
//                 // i = end - 1;
//                 // count.push(Integer.valueOf(s.substring(start, end)));
                
//                 while (s.charAt(i + 1) >= '0' && s.charAt(i + 1) <= '9') {
//                     i++;
//                 }
//                 count.push(Integer.valueOf(s.substring(start, i + 1)));
//                 //System.out.println(count.peek());
//             }
//             else if (c == '[') {
//                 stack.push("");
//             }
//             else if (c == ']') {
//                 StringBuilder sb = new StringBuilder();
//                 int num = count.pop();
//                 String str = stack.pop();
//                 for (int k = 0; k < num; k++) {
//                     sb.append(str);
//                 }
//                 stack.push(stack.pop() + sb.toString());
//             }
//             else {
//                 stack.push(stack.pop() + c);
//             }
//             i++;
//         }
//         return stack.pop();
//     }
// }




class Solution {
    public String decodeString(String s) {
        return helper(s, new int[] {0});
    }
    
    private String helper(String s, int[] start) {
        if (start[0] >= s.length()) {
            return "";
        }
        
        String res = "";
        while (start[0] < s.length() && s.charAt(start[0]) != ']') {
            char c = s.charAt(start[0]);
            if (c < '0' || c > '9') {
                res += c;
                start[0]++;
            }
            else {
                int end = start[0] + 1;
                c = s.charAt(end);
                while (c >= '0' && c <= '9' && end < s.length()) {
                    end++;
                    c = s.charAt(end);
                }
                int num = Integer.valueOf(s.substring(start[0], end));
                
                // int num = 0;
                // c = s.charAt(start[0]);
                // while (c >= '0' && c <= '9' && start[0] < s.length()) {
                //     num = num * 10 + c - '0';
                //     start[0]++;
                //     c = s.charAt(start[0]);
                // }
   
                StringBuilder sb = new StringBuilder();
                
                //s.chatAt[end] = "[" skip '['
                start[0] = end + 1;
                //start[0]++;
                String repeat = helper(s, start);
                //s.chatAt[] = "]" skip "]"
                start[0]++;
                
                
                // for (int i = 0; i < num; i++) {
                //     sb.append(repeat);
                // } 
                while (num > 0) {
                    sb.append(repeat);
                    num--;
                }
                res += sb.toString();
            }
        }
        return res;
    }
}
```





## 733 [Flood Fill](https://leetcode.com/problems/flood-fill)   

```java
// class Solution {
//     private final int[][] DIRECTIONS = {
//         {-1, 0},
//         {1, 0},
//         {0, -1},
//         {0, 1}
//     };
//     public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
//         if (image == null || image.length == 0) {
//             return new int[0][0];
//         }
//         Queue<int[]> queue = new LinkedList();
//         queue.offer(new int[] {sr, sc});
//         int target = image[sr][sc];
//         image[sr][sc] = newColor; // necessary for tail recursion
//         if (newColor == target) {
//             return image;
//         }
//         bfs(image, queue, newColor, target);
//         return image;
//     }
    
//     private void bfs(int[][] image, Queue<int[]> queue, int newColor, int target) {
//         while (!queue.isEmpty()) {
//             int nr = image.length;
//             int nc = image[0].length;
                
//             int[] coordinate = queue.poll();
//             int r = coordinate[0];
//             int c = coordinate[1];
            
//             for (int[] direction : DIRECTIONS) {
//                 int newR = r + direction[0];
//                 int newC = c + direction[1];
//                 if (newR < 0 || newR >= nr || newC < 0 || newC >= nc || image[newR][newC] != target) {
//                     continue;
//                 }
//                 image[newR][newC] = newColor;
//                 queue.offer(new int[] {newR, newC});
//             }
//         }
//     }
// }


// class Solution {
//     private final int[][] DIRECTIONS = {
//         {-1, 0},
//         {1, 0},
//         {0, -1},
//         {0, 1}
//     };
//     public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
//         if (image == null || image.length == 0) {
//             return new int[0][0];
//         }
      
     
//         int target = image[sr][sc];
//         image[sr][sc] = newColor;
//         if (newColor == target) {
//             return image;
//         }
//         dfs(image, newColor, target, sr, sc);
//         return image;
//     }
    
//     private void dfs(int[][] image, int newColor, int target, int r, int c) {
//         int nr = image.length;
//         int nc = image[0].length;
//         for (int[] direction : DIRECTIONS) {
//             int newR = r + direction[0];
//             int newC = c + direction[1];
//             if (newR < 0 || newR >= nr || newC < 0 || newC >= nc || image[newR][newC] != target) {
//                 continue;
//             }
//             image[newR][newC] = newColor;
//             dfs(image, newColor, target, newR, newC);
//         }
//     }
// }


class Solution {
    private final int[][] DIRECTIONS = {
        {-1, 0},
        {1, 0},
        {0, -1},
        {0, 1}
    };
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        if (image == null || image.length == 0) {
            return new int[0][0];
        }
      
     
        int target = image[sr][sc];
        //image[sr][sc] = newColor; Wrong for linear recursion!
        if (newColor == target) {
            return image;
        }
        dfs(image, newColor, target, sr, sc);
        return image;
    }
    
    private void dfs(int[][] image, int newColor, int target, int r, int c) {
        int nr = image.length;
        int nc = image[0].length;
        if (r < 0 || r >= nr || c < 0 || c >= nc || image[r][c] != target) {
            return;
        }
        image[r][c] = newColor;
        
        for (int[] direction : DIRECTIONS) {
            int newR = r + direction[0];
            int newC = c + direction[1];
            dfs(image, newColor, target, newR, newC);
        }
    }
    
//     private void dfs(int[][] image, int newColor, int target, int r, int c) {
//         int nr = image.length;
//         int nc = image[0].length;
//         if (image[r][c] != target) {
//             return;
//         }
        
//         image[r][c] = newColor;
//         for (int[] direction : DIRECTIONS) {
//             int newR = r + direction[0];
//             int newC = c + direction[1];
//             if (newR >= 0 && newR < nr && newC >= 0 && newC < nc) {
//                 dfs(image, newColor, target, newR, newC);
//             }
//         }
//     }
}
```







## 841 [Keys and Rooms](https://leetcode.com/problems/keys-and-rooms)    

```java
// class Solution {
//     public boolean canVisitAllRooms(List<List<Integer>> rooms) {
//         if (rooms.size() <= 0) {
//             return true;
//         }
//         Set<Integer> set = new HashSet();
//         set.add(0);
        
//         bfs(rooms, set, 0);
//         return set.size() == rooms.size();
//     }
    
//     private void bfs(List<List<Integer>> rooms, Set<Integer> set, int index) {
//         Queue<Integer> queue = new LinkedList();
//         for (Integer room : rooms.get(index)) {
//             queue.add(room);
//             set.add(room);
//         }
//         while (!queue.isEmpty()) {
//             Integer key = queue.poll();
//             for (Integer room : rooms.get(key)) {
//                 if (!set.contains(room)) {
//                     queue.offer(room);
//                     set.add(room);
//                 }
//             }
//         }
//     }
// }




// class Solution {
//     public boolean canVisitAllRooms(List<List<Integer>> rooms) {
//         if (rooms.size() <= 0) {
//             return true;
//         }
//         Set<Integer> set = new HashSet();
//         dfs(rooms, set, 0);
//         return set.size() == rooms.size();
//     }
    
//     private void dfs(List<List<Integer>> rooms, Set<Integer> set, int index) {
//         set.add(index);
//         for (Integer room : rooms.get(index)) {
//             if (!set.contains(room)) {
//                 dfs(rooms, set, room);
//             }
//         }
//     }
// }


// class Solution {
//     public boolean canVisitAllRooms(List<List<Integer>> rooms) {
//         if (rooms.size() <= 0) {
//             return true;
//         }
//         Set<Integer> set = new HashSet();
//         set.add(0);
        
//         dfs(rooms, set, 0);
//         return set.size() == rooms.size();
//     }
    
//     private void dfs(List<List<Integer>> rooms, Set<Integer> set, int index) {
//         for (Integer room : rooms.get(index)) {
//             if (!set.contains(room)) {
//                 set.add(room);
//                 dfs(rooms, set, room);
//             }
//         }
//     }
// }


class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        if (rooms.size() <= 0) {
            return true;
        }
        Set<Integer> set = new HashSet();
        Stack<Integer> stack = new Stack();
        set.add(0);
        stack.push(0);
        
        while (!stack.isEmpty()) {
            for (Integer room : rooms.get(stack.pop())) {
                if (!set.contains(room)) {
                    set.add(room);
                    stack.push(room);
                    if (set.size() == rooms.size()) {return true;} //one more step less：pruning
                }
            }
        }
        return set.size() == rooms.size();
    }
}



//O(N + E) N: ROOM E: N of unique keys

// class Solution {
//     public boolean canVisitAllRooms(List<List<Integer>> rooms) {
//         if (rooms.size() <= 0) {
//             return true;
//         }
//         boolean[] seen = new boolean[rooms.size()];
//         Stack<Integer> stack = new Stack();
//         stack.push(0);
//         seen[0] = true;

           //O(E)
//         while (!stack.isEmpty()) { 
//             for (Integer room : rooms.get(stack.pop())) {
//                 if (seen[room] == false) {
//                     seen[room] = true;
//                     stack.push(room);
//                 }
                
//             }
//         }
           //O(N)
//         for (boolean element : seen) {  
//             if (element == false) {
//                 return false;
//             }
//         }
//         return true;
//     }
// }
```



