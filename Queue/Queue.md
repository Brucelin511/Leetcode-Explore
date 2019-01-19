## 622[Design Circular Queue](https://leetcode.com/problems/design-circular-queue/)

```java
class MyCircularQueue {
    int[] arr;
    int head;
    int tail;
    int k;
    
    /** Initialize your data structure here. Set the size of the queue to be k. */
    public MyCircularQueue(int k) {
        arr = new int[k];
        head = -1;
        tail = -1;
        this.k = k;
    }
    
    /** Insert an element into the circular queue. Return true if the operation is successful. */
    public boolean enQueue(int value) {
        if (isFull() == true) {
       
            return false;
        }
        if (isEmpty() == true) {
            head = 0;
        }
        tail = (tail + 1) % k;
        arr[tail] = value;
    
        return true;
    }
    
    /** Delete an element from the circular queue. Return true if the operation is successful. */
    public boolean deQueue() {
        if (isEmpty() == true) {
        
            return false;
        }
        if (head == tail) {
            head = -1;
            tail = -1;
        } else {
            head = (head + 1) % k;
        }
     
        return true;
    }
    
    /** Get the front item from the queue. */
    public int Front() {
        if (isEmpty()) {
            return -1;
        }
        return arr[head];
    }
    
    /** Get the last item from the queue. */
    public int Rear() {
        if (isEmpty()) {
            return -1;
        }
        return arr[tail];
        
    }
    
    /** Checks whether the circular queue is empty or not. */
    public boolean isEmpty() {

        return head == -1;
    }
    
    /** Checks whether the circular queue is full or not. */
    public boolean isFull() {

        return (tail + 1) % k == head;
    }
    
    // private void print() {
    //     System.out.println("head:" + head);
    //     System.out.println("tail:" + tail);
    //     for (int element : arr) {
    //         System.out.print(element);
    //     }
    //     System.out.println();
    //     System.out.println();
    //     System.out.println();
    // }
}

/**
 * Your MyCircularQueue object will be instantiated and called as such:
 * MyCircularQueue obj = new MyCircularQueue(k);
 * boolean param_1 = obj.enQueue(value);
 * boolean param_2 = obj.deQueue();
 * int param_3 = obj.Front();
 * int param_4 = obj.Rear();
 * boolean param_5 = obj.isEmpty();
 * boolean param_6 = obj.isFull();
 */
```







## 346[Moving Average from Data Stream](https://leetcode.com/problems/moving-average-from-data-stream)

```java
class MovingAverage {
    
    Queue<Integer> queue;
    int size;
    int sum;
    /** Initialize your data structure here. */
    public MovingAverage(int size) {
        queue = new LinkedList();
        this.size = size;
        sum = 0;
    }
    
    public double next(int val) {
        if (queue.size() == size) {
            sum -= queue.poll();
        }
        queue.offer(val);
        sum += val;
        return (double) sum / queue.size();
    }
}


// class MovingAverage {
    
//     int[] arr;
//     int sum;
//     int insert;
//     int n;
//     /** Initialize your data structure here. */
//     public MovingAverage(int size) {
//         arr = new int[size];
//         insert = 0;
//         sum = 0;
//         n = 0;
//     }
    
//     public double next(int val) {
//         if (n < arr.length) {
//             n++;
//         }
//         sum -= arr[insert];
//         sum += val;
//         arr[insert] = val;
//         insert = (insert + 1) % arr.length;
//         return (double) sum / n;
//     }
// }

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage obj = new MovingAverage(size);
 * double param_1 = obj.next(val);
 */
```





## 286[Walls and Gates](https://leetcode.com/problems/walls-and-gates) 

```java
class Solution {
    private static final int EMPTY = Integer.MAX_VALUE;
    private static final int GATE = 0;
    private static final int WALL = -1;
    private static final int[][] DIRECTIONS = {
        {-1, 0},
        {1, 0},
        {0, -1},
        {0, 1},
    };
    // private static final List<int[]> DIRECTIONS = Arrays.asList(
    //     new int[] {-1, 0},
    //     new int[] {1, 0},
    //     new int[] {0, -1},
    //     new int[] {0, 1}
    // );
    
    public void wallsAndGates(int[][] rooms) {
        if (rooms == null || rooms.length == 0 || rooms[0].length == 0) {
            return;
        }
        
        Queue<int[]> queue = new LinkedList();
        for (int i = 0; i < rooms.length; i++) {
            for (int j = 0; j < rooms[0].length; j++) {
                if (rooms[i][j] == GATE) {
                    queue.add(new int[] {i, j});
                }
            }
        }
        
        bfs(rooms, queue);
        
    }
    
    private int bfs(int[][] rooms, Queue<int[]> queue) {
        int nr = rooms.length;
        int nc = rooms[0].length;
        
        while (!queue.isEmpty()) {
            int[] coordinate = queue.poll();
            int r = coordinate[0];
            int c = coordinate[1];
            // for (int i = 0; i < 4; i++) {
            //     int newR = r + DIRECTIONS[i][0];
            //     int newC = r + DIRECTIONS[i][1];
            // }
            for (int[] element : DIRECTIONS) {
                int newR = r + element[0];
                int newC = c + element[1];
                if (newR < 0 || newR >= nr || newC < 0 || newC >= nc || rooms[newR][newC] != EMPTY) {       
                    continue;
                }
                rooms[newR][newC] = rooms[r][c] + 1;
                queue.offer(new int[] {newR, newC});
            }
        }
        return Integer.MAX_VALUE;
    }
    
//     public void wallsAndGates(int[][] rooms) {
//         if (rooms == null || rooms.length == 0 || rooms[0].length == 0) {
//             return;
//         }
        
//         for (int i = 0; i < rooms.length; i++) {
//             for (int j = 0; j < rooms[0].length; j++) {
//                 if (rooms[i][j] == EMPTY) {
//                     rooms[i][j] = bfs(rooms, i, j);
//                 }
//             }
//         }
//     }
    
//     private int bfs(int[][] rooms, int i, int j) {
//         Queue<int[]> queue = new LinkedList();
//         queue.add(new int[] {i, j});
//         int nr = rooms.length;
//         int nc = rooms[0].length;
//         int[][] distance = new int[nr][nc];
        
//         while (!queue.isEmpty()) {
//             int[] coordinate = queue.poll();
//             int r = coordinate[0];
//             int c = coordinate[1];
//             // for (int i = 0; i < 4; i++) {
//             //     int newR = r + DIRECTIONS[i][0];
//             //     int newC = r + DIRECTIONS[i][1];
//             // }
//             for (int[] element : DIRECTIONS) {
//                 int newR = r + element[0];
//                 int newC = c + element[1];
//                 if (newR < 0 || newR >= nr || newC < 0 || newC >= nc || rooms[newR][newC] == WALL || distance[newR][newC] != 0) {       
//                     continue;
//                 }
                
//                 distance[newR][newC] = distance[r][c] + 1;
                
//                 if (rooms[newR][newC] == GATE) {
//                     return distance[newR][newC];
//                 }
//                 queue.offer(new int[] {newR, newC});
//             }
//         }
//         return Integer.MAX_VALUE;
//     }
}
```









## 200 [Number of Islands](https://leetcode.com/problems/number-of-islands) 

```
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



## 755[Open the Lock](https://leetcode.com/problems/open-the-lock)    

```
// class Solution {
//     public int openLock(String[] deadends, String target) {
//         Queue<String> queue = new LinkedList();
//         Set<String> deadendsSet = new HashSet<String>(Arrays.asList(deadends));
        
//         // make sure there is no deadends in queue
//         if (deadendsSet.contains("0000")){
//             return -1;
//         }
//         Set<String> set = new HashSet();
//         queue.offer("0000");
//         queue.offer(null);
        
//         set.add("0000");
//         int count = 0;
        
//         while (!queue.isEmpty()) {
//             String head = queue.poll();
//             if (head == null) {
//                 if (queue.peek() != null){
//                     count++;
//                     queue.offer(null); 
//                 } 
//                 continue;
//             }
            
//             if (head.equals(target)) {
//                 return count;
//             }

//             // if it can be sure that there is no deadends in queue, there is no need to check anymore!
//             // if (deadendsSet.contains(head)) {
//             //     continue;
//             // }
            
//             String[] array = getChange(head);
//             for (String str : array) {
//                 if (!set.contains(str) && !deadendsSet.contains(str)) { // make sure there is no deadends in queue
//                     queue.offer(str);
//                     set.add(str);
//                 }
//             }
//         }
        
//         // while (!queue.isEmpty()) {
//         //     String head = queue.poll();
//         //     if (head == null) {
//         //         if (queue.peek() != null){
//         //             count++;
//         //             queue.offer(null);
//         //         }
//         //     }
//         //     else if (head.equals(target)) {
//         //         return count;
//         //     }
//         //     else if (!deadendsSet.contains(head)) {            
//         //         String[] array = getChange(head);
//         //         for (String str : array) {
//         //             if (!set.contains(str)) {
//         //                 queue.offer(str);
//         //                 set.add(str);
//         //             }
//         //         }
//         //     }
//         // }
        
//         return -1;
//     }
    
//     private String[] getChange(String head) {
//         String[] res = new String[8];
//         for (int i = 0; i < 4; i++) {
//             res[2 * i + 0] = head.substring(0, i) + (head.charAt(i) - '0' - 1 + 10) % 10 + head.substring(i + 1, 4);
//             res[2 * i + 1] = head.substring(0, i) + (head.charAt(i) - '0' + 1 + 10) % 10 + head.substring(i + 1, 4);
//         }
//         return res;
//     }
// }


class Solution {
    public int openLock(String[] deadends, String target) {
        Queue<String> queue = new LinkedList();
        Set<String> deadendsSet = new HashSet<String>(Arrays.asList(deadends));
        
        // make sure there is no deadends in queue
        if (deadendsSet.contains("0000")){
            return -1;
        }
        
        Set<String> set = new HashSet();
        queue.offer("0000");
        deadendsSet.add("0000");
        int count = 0;
        
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            while (size > 0) {
                String head = queue.poll();
                if (head.equals(target)) {
                    return count;
                }
                
                // if (deadendsSet.contains(head)) {
                //     size--;
                //     continue;
                // }

                String[] array = getChange(head);
                for (String str : array) {
                    if (!deadendsSet.contains(str)) { // make sure there is no deadends in queue
                        queue.offer(str);
                        deadendsSet.add(str);
                    }
                }
                size--;
            }
            count++;
        }
        
        return -1;
    }
    
    private String[] getChange(String head) {
        String[] res = new String[8];
        for (int i = 0; i < 4; i++) {
            res[2 * i + 0] = head.substring(0, i) + (head.charAt(i) - '0' - 1 + 10) % 10 + head.substring(i + 1, 4);
            res[2 * i + 1] = head.substring(0, i) + (head.charAt(i) - '0' + 1 + 10) % 10 + head.substring(i + 1, 4);
        }
        return res;
    }
}


// class Solution {
//     public int openLock(String[] deadends, String target) {
//         Set<String> begin = new HashSet();
//         Set<String> end = new HashSet();
//         Set<String> deadendsSet = new HashSet<String>(Arrays.asList(deadends));
        
//         // make sure there is no deadends in queue
//         if (deadendsSet.contains("0000")){
//             return -1;
//         }
        
//         begin.add("0000");
//         end.add(target);
//         int count = 0;
        
//         while (!begin.isEmpty()) {
//             Set<String> temp;
//             if (begin.size() > end.size()){
//                 temp = begin;
//                 begin = end;
//                 end = temp;
//             }
//             temp = new HashSet();
//             for (String element : begin){
//                 if (end.contains(element)) {
//                     return count;
//                 }
//                 if (deadendsSet.contains(element)){
//                     continue;
//                 }
//                 deadendsSet.add(element);
//                 for (String str : getChange(element)) {
//                     if (!deadendsSet.contains(str)) {
//                         temp.add(str);
//                         //wrong: deadendsSet.add(str); why???
//                     }
//                 }
//             }
//             count++;
//             begin = temp;
            
// //             begin = end;
// //             end = temp;
//         }
        
//         return -1;
//     }
    
//     private String[] getChange(String head) {
//         String[] res = new String[8];
//         StringBuilder sb = new StringBuilder(head);
//         for (int i = 0; i < 4; i++) {
//             res[2 * i + 0] = sb.substring(0, i) + (head.charAt(i) - '0' - 1 + 10) % 10 + sb.substring(i + 1, 4);
//             res[2 * i + 1] = sb.substring(0, i) + (head.charAt(i) - '0' + 1 + 10) % 10 + sb.substring(i + 1, 4);
//         }
//         return res;
//     }
// }




// class Solution {
//     public int openLock(String[] deadends, String target) {
//         Set<String> begin = new HashSet<>();
//         Set<String> end = new HashSet<>();
//         Set<String> deads = new HashSet<>(Arrays.asList(deadends));
//         begin.add("0000");
//         end.add(target);
//         int level = 0;
//         Set<String> temp;
//         while(!begin.isEmpty() && !end.isEmpty()) {
//             if (begin.size() > end.size()) {
//                 temp = begin;
//                 begin = end;
//                 end = temp;
//             }
//             temp = new HashSet<>();
//             for(String s : begin) {
//                 if(end.contains(s)) return level;
//                 if(deads.contains(s)) continue;
//                 deads.add(s);
//                 StringBuilder sb = new StringBuilder(s);
//                 for(int i = 0; i < 4; i ++) {
//                     char c = sb.charAt(i);
//                     String s1 = sb.substring(0, i) + (c == '9' ? 0 : c - '0' + 1) + sb.substring(i + 1);
//                     String s2 = sb.substring(0, i) + (c == '0' ? 9 : c - '0' - 1) + sb.substring(i + 1);
//                     if(!deads.contains(s1))
//                         temp.add(s1);
//                     if(!deads.contains(s2))
//                         temp.add(s2);
//                 }
//             }
//             level ++;
//             begin = temp;
//         }
//         return -1;
//     }
// }
```









## 279 [Perfect Squares](https://leetcode.com/problems/perfect-squares)

```java
// class Solution {
//     public int numSquares(int n) {
//         List<Integer> list = new ArrayList();
//         int[] step = new int[n + 1]; // 0 - n
        
//         for (int i = 1; i * i <= n; i++) {
//             list.add(i * i);
//         }
        
//         Queue<Integer> queue = new LinkedList();
//         queue.offer(0);
//         queue.offer(null);
        
//         int level = 0;
//         while (!queue.isEmpty()) {
//             Integer curr = queue.poll();
//             //System.out.print(curr);
//             if (curr == null) {
//                 level++;
//                 queue.offer(null);
//             }
//             else if (curr == n) {
//                 return level;
//             }
//             else {
//                 for (Integer element : list) {
//                     if (curr + element > n) {
//                         break;
//                     }
//                     if (step[curr + element] == 0) {
//                         step[curr + element] = step[curr] + 1;
//                         queue.offer(curr + element);
//                     }
//                 }
//                 // if (queue.peek() == null) {
//                 //     queue.offer(null);
//                 // }
//             }
//         }
//         return 0;
//     }
// }



// class Solution {
//     public int numSquares(int n) {
//         List<Integer> list = new ArrayList();
//         int[] step = new int[n + 1]; // 0 - n
        
//         for (int i = 1; i * i <= n; i++) {
//             list.add(i * i);
//         }
        
//         Queue<Integer> queue = new LinkedList();
//         queue.offer(0);
//         queue.offer(null);
        
//         int level = 0;
//         while (!queue.isEmpty()) {
//             Integer curr = queue.poll();
//             //System.out.print(curr);
//             if (curr == null) {
//                 level++;
//                 queue.offer(null);
//             } 
//             else {
//                 for (Integer element : list) {
//                     if (curr + element > n) {
//                         break;
//                     }
//                     if (step[curr + element] == 0) {
//                         step[curr + element] = step[curr] + 1;
//                         if (curr + element == n) {
//                             return level + 1;
//                             //return step[n];
//                         } 
//                         queue.offer(curr + element);
//                     }
//                 }
//             }
//         }
//         return 0;
//     }
// }



// class Solution {
//     public int numSquares(int n) {
//         List<Integer> list = new ArrayList();
//         int[] step = new int[n + 1]; // 0 - n
        
//         for (int i = 1; i * i <= n; i++) {
//             list.add(i * i);
//         }
        
//         Queue<Integer> queue = new LinkedList();
//         queue.offer(0);
        
//         int level = 0;
//         while (!queue.isEmpty()) {
//             //System.out.print(curr);
//             int size = queue.size();
//             for (int i = 0; i < size; i++) {
//                 Integer curr = queue.poll();
//                 if (curr == n) {
//                     return level;
//                     //return step[n];
//                 }
//                 else {
//                     for (Integer element : list) {
//                         if (curr + element > n) {
//                             break;
//                         }
//                         if (step[curr + element] == 0) {
//                             step[curr + element] = step[curr] + 1;
//                             queue.offer(curr + element);
//                         }
//                     }
//                 }
//             }
//             level++;
//         }
//         return 0;
//     }
// }



// class Solution {
//     public int numSquares(int n) {
//         List<Integer> list = new ArrayList();
//         int[] step = new int[n + 1]; // 0 - n
        
//         for (int i = 1; i * i <= n; i++) {
//             list.add(i * i);
//         }
        
//         Queue<Integer> queue = new LinkedList();
//         queue.offer(0);
        
//         int level = 0;
//         while (!queue.isEmpty()) {
//             //System.out.print(curr);
//             level++;
//             int size = queue.size();
//             for (int i = 0; i < size; i++) {
//                 Integer curr = queue.poll();
//                 if (curr == n) {   //not pruning => slow
//                     return level - 1; 
//                     //return step[n];
//                 }
//                 else {
//                     for (Integer element : list) {
//                         if (curr + element > n) {
//                             break;
//                         }
//                         if (step[curr + element] == 0) {
//                             step[curr + element] = step[curr] + 1;
//                             queue.offer(curr + element);
//                         }
//                     }
//                 }
//             }
//         }
//         return 0;
//     }
// }



class Solution {
    public int numSquares(int n) {
        List<Integer> list = new ArrayList();
        int[] step = new int[n + 1]; // 0 - n
        
        for (int i = 1; i * i <= n; i++) {
            list.add(i * i);
        }
        
        Queue<Integer> queue = new LinkedList();
        queue.offer(0);
        
        int level = 0;
        while (!queue.isEmpty()) {
            //System.out.print(curr);
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                Integer curr = queue.poll();
                for (Integer element : list) {
                    if (curr + element > n) {
                        break;
                    }
                    if (step[curr + element] == 0) {
                        step[curr + element] = step[curr] + 1;
                        if (curr + element == n){  //pruning => fast
                            return level + 1;
                            //return step[n];
                        }
                        queue.offer(curr + element);
                    }
                }
            }
            level++;
        }
        return 0;
    }
}


// class Solution {
//     public int numSquares(int n) {
//         List<Integer> list = new ArrayList();
//         int[] step = new int[n + 1]; // 0 - n
        
//         for (int i = 1; i * i <= n; i++) {
//             list.add(i * i);
//         }
        
//         Queue<Integer> queue = new LinkedList();
//         queue.offer(0);
        
//         int level = 0;
//         while (!queue.isEmpty()) {
//             //System.out.print(curr);
//             level++;
//             int size = queue.size();
//             for (int i = 0; i < size; i++) {
//                 Integer curr = queue.poll();
//                 for (Integer element : list) {
//                     if (curr + element > n) {
//                         break;
//                     }
//                     if (step[curr + element] == 0) {
//                         step[curr + element] = step[curr] + 1;
//                         if (curr + element == n){
//                             return level;
//                             //return step[n];
//                         }
//                         queue.offer(curr + element);
//                     }
//                 }
//             }
//         }
//         return 0;
//     }
// }


//summary the position of level++ and return level level - 1 and level + 1
//return step[n] is always right!
```









## 225[Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues)   

```java

// class MyStack {
//     Queue<Integer> queue;
//     int top;
//     /** Initialize your data structure here. */
//     public MyStack() {
//         queue = new LinkedList();
//     }
    
//     /** Push element x onto stack. */
//     public void push(int x) {
//         queue.offer(x);
//         top = x;
//     }
    
//     /** Removes the element on top of the stack and returns that element. */
//     public int pop() {
//         Queue<Integer> temp = new LinkedList();
//         while (queue.size() > 1) {
//             top = queue.poll();
//             temp.offer(top);
//         }
        
//         // Queue<Integer> temp = new LinkedList();
//         // while (queue.size() > 2) {
//         //     temp.offer(queue.poll());
//         // }
//         // if (queue.size() == 2) {
//         //     top = queue.poll();
//         //     temp.offer(top);
//         // }
        
//         int res = queue.poll();
//         queue = temp;
        
//         return res;
//     }
    
//     /** Get the top element. */
//     public int top() {
//         // if (empty()) {
//         //     return -1;
//         // }
        
//         // Queue<Integer> temp = new LinkedList();
//         // while (queue.size() > 1) {
//         //     temp.offer(queue.poll());
//         // }
//         // int res = queue.poll();
//         // temp.offer(res);
//         // queue = temp;
//         // return res;
        
//         return top;
//     }
    
//     /** Returns whether the stack is empty. */
//     public boolean empty() {
//         return queue.isEmpty();
//     }
// }

// /**
//  * Your MyStack object will be instantiated and called as such:
//  * MyStack obj = new MyStack();
//  * obj.push(x);
//  * int param_2 = obj.pop();
//  * int param_3 = obj.top();
//  * boolean param_4 = obj.empty();
//  */






class MyStack {
    Queue<Integer> queue;
    Queue<Integer> temp;
    int top;
    /** Initialize your data structure here. */
    public MyStack() {
        queue = new LinkedList();
        temp = new LinkedList();
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        temp.offer(x);
        top = x;
        while (!queue.isEmpty()) {
            temp.offer(queue.poll());
        }
        Queue<Integer> t = queue;
        queue = temp;
        temp = t;
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        int res = queue.poll();
        if (!queue.isEmpty()) {
            top = queue.peek();
        }
        return res;
    }
    
    /** Get the top element. */
    public int top() {
        return top;
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return queue.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */




// class MyStack {
//     Queue<Integer> queue;
//     int top;
//     /** Initialize your data structure here. */
//     public MyStack() {
//         queue = new LinkedList();
//     }
    
//     /** Push element x onto stack. */
//     public void push(int x) {
//         top = x;
//         queue.offer(x);
//         int size = queue.size();
//         while (size > 1) {
//             queue.offer(queue.poll());
//             size--;
//         }
//     }
    
//     /** Removes the element on top of the stack and returns that element. */
//     public int pop() {
//         int res = queue.poll();
//         if (!queue.isEmpty()) {
//             top = queue.peek();
//         }
//         return res;
//     }
    
//     /** Get the top element. */
//     public int top() {
//         return top;
//     }
    
//     /** Returns whether the stack is empty. */
//     public boolean empty() {
//         return queue.isEmpty();
//     }
// }

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```







## 733 [Flood Fill](https://leetcode.com/problems/flood-fill) 

```java
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
         Queue<int[]> queue = new LinkedList();
         queue.offer(new int[] {sr, sc});
         int target = image[sr][sc];
         image[sr][sc] = newColor; // necessary for tail recursion
         if (newColor == target) {
             return image;
         }
         bfs(image, queue, newColor, target);
         return image;
     }
    
     private void bfs(int[][] image, Queue<int[]> queue, int newColor, int target) {
         while (!queue.isEmpty()) {
             int nr = image.length;
             int nc = image[0].length;
                
             int[] coordinate = queue.poll();
             int r = coordinate[0];
             int c = coordinate[1];
            
             for (int[] direction : DIRECTIONS) {
                 int newR = r + direction[0];
                 int newC = c + direction[1];
                 if (newR < 0 || newR >= nr || newC < 0 || newC >= nc || image[newR][newC] != target) {
                     continue;
                 }
                 image[newR][newC] = newColor;
                 queue.offer(new int[] {newR, newC});
             }
         }
     }
 }
```







## 542 [01 Matrix](https://leetcode.com/problems/01-matrix)    

```java
// class Solution {
//     private final int[][] DIRECTION = {
//         {1,0},
//         {-1,0},
//         {0,1},
//         {0,-1}
//     };
    
//     public int[][] updateMatrix(int[][] matrix) {
//         if (matrix == null) {
//             return null;
//         }
//         int nr = matrix.length;
//         if (nr == 0) {
//             return new int[0][0];
//         }
//         //O(N) space 
//         int nc = matrix[0].length;
        
//         int[][] res = new int[nr][nc];
//         for (int[] row : res) {
//             Arrays.fill(row, Integer.MAX_VALUE);
//         }
        
//         Queue<int[]> queue = new LinkedList();
//         for (int i = 0; i < nr; i++) {
//             for (int j = 0; j < nc; j++) {
//                 if (matrix[i][j] == 0) {
//                     queue.add(new int[]{i, j});
//                     res[i][j] = 0;
//                 }
//             }
//         }
//         bfs(matrix, res, queue);
//         return res;
//     }
    
//     private void bfs(int[][] matrix, int[][] res, Queue<int[]> queue) {
//         while (!queue.isEmpty()) {
//             int[] coordinate = queue.poll();
//             int r = coordinate[0];
//             int c = coordinate[1];
//             for (int[] element : DIRECTION) {
//                 int newR = r + element[0];
//                 int newC = c + element[1];
//                 // if (newR < 0 || newR >= matrix.length || newC < 0 || newC >= matrix[0].length || matrix[newR][newC] == 0) {
//                 //     continue;
//                 // }
//                 // res[newR][newC] = res[r][c] + 1;
//                 // matrix[newR][newC] = 0;
                
                
//                 //if (newR < 0 || newR >= matrix.length || newC < 0 || newC >= matrix[0].length || res[r][c] + 1 >= res[newR][newC]) {
                
            
//                 if (newR < 0 || newR >= matrix.length || newC < 0 || newC >= matrix[0].length || res[r][c] + 1 >= res[newR][newC]) {
//                     continue;
//                 }
//                 res[newR][newC] = res[r][c] + 1;
                
//                 queue.add(new int[] {newR, newC});
//             }
//         }
//     }
// }


//note do not use set<int[]> because contains take o(n)


// class Solution {
//     private final int[][] DIRECTION = {
//         {1,0},
//         {-1,0},
//         {0,1},
//         {0,-1}
//     };
    
//     public int[][] updateMatrix(int[][] matrix) {
//         if (matrix == null) {
//             return null;
//         }
//         int nr = matrix.length;
//         if (nr == 0) {
//             return new int[0][0];
//         }
//         //O(N) space 
//         int nc = matrix[0].length;
        
//         Queue<int[]> queue = new LinkedList();
        
//         for (int i = 0; i < nr; i++) {
//             for (int j = 0; j < nc; j++) {
//                 if (matrix[i][j] == 1) {
//                     matrix[i][j] = Integer.MIN_VALUE;
//                 } else {
//                     queue.add(new int[]{i, j});
//                 }
//             }
//         }
        
//         bfs(matrix, queue);
//         return matrix;
//     }
    
//     private void bfs(int[][] matrix, Queue<int[]> queue) {
//         while (!queue.isEmpty()) {
//             int[] coordinate = queue.poll();
//             int r = coordinate[0];
//             int c = coordinate[1];
//             for (int[] element : DIRECTION) {
//                 int newR = r + element[0];
//                 int newC = c + element[1];
//                 if (newR < 0 || newR >= matrix.length || newC < 0 || newC >= matrix[0].length || matrix[newR][newC] != Integer.MIN_VALUE) {
//                     continue;
//                 }
//                 matrix[newR][newC] = matrix[r][c] + 1; 
//                 queue.add(new int[] {newR, newC});
//             }
//         }
//     }
// }


class Solution {
    private final int[][] DIRECTION = {
        {1,0},
        {-1,0},
        {0,1},
        {0,-1}
    };
    
    public int[][] updateMatrix(int[][] matrix) {
        if (matrix == null) {
            return null;
        }
        int nr = matrix.length;
        if (nr == 0) {
            return new int[0][0];
        }
        //O(N) space 
        int nc = matrix[0].length;
        
        Queue<int[]> queue = new LinkedList();
        
        for (int i = 0; i < nr; i++) {
            for (int j = 0; j < nc; j++) {
                if (matrix[i][j] == 1) {
                    matrix[i][j] = Integer.MAX_VALUE;
                } else {
                    queue.add(new int[]{i, j});
                }
            }
        }
        
        bfs(matrix, queue);
        return matrix;
    }
    
    private void bfs(int[][] matrix, Queue<int[]> queue) {
        while (!queue.isEmpty()) {
            int[] coordinate = queue.poll();
            int r = coordinate[0];
            int c = coordinate[1];
            for (int[] element : DIRECTION) {
                int newR = r + element[0];
                int newC = c + element[1];
                //if (newR < 0 || newR >= matrix.length || newC < 0 || newC >= matrix[0].length || matrix[newR][newC] != Integer.MAX_VALUE) {
                if (newR < 0 || newR >= matrix.length || newC < 0 || newC >= matrix[0].length ||  matrix[r][c] + 1 >= matrix[newR][newC]) {
                    continue;
                }
                matrix[newR][newC] = matrix[r][c] + 1; 
                queue.add(new int[] {newR, newC});
            }
        }
    }
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

