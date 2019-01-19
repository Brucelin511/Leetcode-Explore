## 705 [Design HashSet](https://leetcode.com/problems/design-hashset)    

```java
// class MyHashSet {
//     boolean[] array;
//     /** Initialize your data structure here. */
//     public MyHashSet() {
//         array = new boolean[1000001];
//     }
    
//     // O(1)
//     public void add(int key) {
//         if (!contains(key)) {
//             array[key] = true;
//         }
//     }
    
//     // O(1)
//     public void remove(int key) {
//         if (contains(key)) {
//             array[key] = false;
//         }
//     }
    
//     /** Returns true if this set contains the specified element */
//     // O(1)
//     public boolean contains(int key) {
//         return array[key];
//     }
// }

// /**
//  * Your MyHashSet object will be instantiated and called as such:
//  * MyHashSet obj = new MyHashSet();
//  * obj.add(key);
//  * obj.remove(key);
//  * boolean param_3 = obj.contains(key);
//  */



class MyHashSet {
    int buckets = 1000;
    //int maxItemsPerBucket = 1001; //=> key / buckets;  (1000k is the 1001th)
    int maxItemsPerBucket = 1000; //=> (key - 1) / buckets;  (1000k is the 1000th)
    boolean[][] array;
    
    /** Initialize your data structure here. */
    public MyHashSet() {
        array = new boolean[buckets][];
    }
    
    // O(1)
    public void add(int key) {
        if (contains(key)) { 
            return;
        }
        if (array[hash(key)] == null) {
            array[hash(key)] = new boolean[maxItemsPerBucket];
        }
        array[hash(key)][pos(key)] = true;
    }
    
    // O(1)
    public void remove(int key) {
        if (!contains(key)) {
            return;
        }
        array[hash(key)][pos(key)] = false;
    }
    
    /** Returns true if this set contains the specified element */
    // O(1)
    public boolean contains(int key) {
        return array[hash(key)] != null && array[hash(key)][pos(key)];
    }
    
    private int hash(int key) {
        return key % buckets;
    }
    
    private int pos(int key) {
        return (key - 1) / buckets;
        //return key / buckets;
    }
}

/**
 * Your MyHashSet object will be instantiated and called as such:
 * MyHashSet obj = new MyHashSet();
 * obj.add(key);
 * obj.remove(key);
 * boolean param_3 = obj.contains(key);
 */
```



## 706 [Design HashMap](https://leetcode.com/problems/design-hashmap)   

```java
// class MyHashMap {
//     int bucket = 1000;
//     int maxItemsPerbucket = 1000;
//     int[][][] table;
    
//     /** Initialize your data structure here. */
//     public MyHashMap() {
//         table = new int[bucket][][];
//     }
    
//     /** value will always be non-negative. */
//     public void put(int key, int value) {
//         // //wrong!!! = contains => update!
//         // // if (contains(key)) {
//         // //     return;
//         // // }
//         // if (table[hash(key)] == null) {
//         //     table[hash(key)] = new int[maxItemsPerbucket][];
//         // }
//         // table[hash(key)][pos(key)] = new int[] {key, value};
        
//         //update
//         if (contains(key)) {
//             table[hash(key)][pos(key)][1] = value;
//             return;
//         }
//         //create new one
//         if (table[hash(key)] == null) {
//             table[hash(key)] = new int[maxItemsPerbucket][];
//         }
//         table[hash(key)][pos(key)] = new int[] {key, value};
//     }
    
//     /** Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key */
//     public int get(int key) {
//         if (!contains(key)) {
//             return -1;
//         }
//         return table[hash(key)][pos(key)][1];
//     }
    
//     /** Removes the mapping of the specified value key if this map contains a mapping for the key */
//     public void remove(int key) {
//         if (!contains(key)) {
//             return;
//         }
//         table[hash(key)][pos(key)] = null;
//     }
    
//     private boolean contains(int key) {
//         return table[hash(key)] != null && table[hash(key)][pos(key)] != null;
//     }
    
//     private int hash(int key) {
//         return key % bucket;
//     }
    
//     private int pos(int key) {
//         return (key - 1) / bucket;
//     }
// }

// /**
//  * Your MyHashMap object will be instantiated and called as such:
//  * MyHashMap obj = new MyHashMap();
//  * obj.put(key,value);
//  * int param_2 = obj.get(key);
//  * obj.remove(key);
//  */


// class MyHashMap {
//     private class element {
//         int key;
//         int value;
//         element (int key, int value) {
//             this.key = key;
//             this.value = value;
//         }
//     }
    
//     int bucket = 1000;
//     int maxItemsPerbucket = 1000;
//     element[][] table;
    
    
//     /** Initialize your data structure here. */
//     public MyHashMap() {
//         table = new element[bucket][];
//     }
    
//     /** value will always be non-negative. */
//     public void put(int key, int value) {
//         // //wrong!!! = contains => update!
//         // // if (contains(key)) {
//         // //     return;
//         // // }
//         // if (table[hash(key)] == null) {
//         //     table[hash(key)] = new int[maxItemsPerbucket][];
//         // }
//         // table[hash(key)][pos(key)] = new int[] {key, value};
        
//         //update
//         if (contains(key)) {
//             table[hash(key)][pos(key)].value = value;
//             return;
//         }
//         //create new one
//         if (table[hash(key)] == null) {
//             table[hash(key)] = new element[maxItemsPerbucket];
//         }
//         table[hash(key)][pos(key)] = new element(key, value);
//     }
    
//     /** Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key */
//     public int get(int key) {
//         if (!contains(key)) {
//             return -1;
//         }
//         return table[hash(key)][pos(key)].value;
//     }
    
//     /** Removes the mapping of the specified value key if this map contains a mapping for the key */
//     public void remove(int key) {
//         if (!contains(key)) {
//             return;
//         }
//         table[hash(key)][pos(key)] = null;
//     }
    
//     private boolean contains(int key) {
//         return table[hash(key)] != null && table[hash(key)][pos(key)] != null;
//     }
    
//     private int hash(int key) {
//         return key % bucket;
//     }
    
//     private int pos(int key) {
//         return (key - 1) / bucket;
//     }
// }

// /**
//  * Your MyHashMap object will be instantiated and called as such:
//  * MyHashMap obj = new MyHashMap();
//  * obj.put(key,value);
//  * int param_2 = obj.get(key);
//  * obj.remove(key);
//  */


class MyHashMap {
    private class ListNode {
        int key, val;
        ListNode next;
        ListNode (int key, int val) {
            this.key = key;
            this.val = val;
        }
    }
    
    int bucket = 100000;
    ListNode[] table;
    /** Initialize your data structure here. */
    public MyHashMap() {
        table = new ListNode[bucket];
    }
    
    /** value will always be non-negative. */
    public void put(int key, int value) {
        //check whether the bucket is null, if null then create new one
        if (table[hash(key)] == null) {
            table[hash(key)] = new ListNode(0, 0);
        }
        
        //update
        ListNode pre = findPre(table[hash(key)], key);
        if (pre.next != null) {
            pre.next.key = key;
            pre.next.val = value;
        }
        else {
            pre.next = new ListNode(key, value);
        }
    }
    
    /** Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key */
    public int get(int key) {
        ListNode pre = findPre(table[hash(key)], key);
        if (pre == null || pre.next == null) {
            return -1;
        }
        else {
            return pre.next.val;
        }
    }
    
    /** Removes the mapping of the specified value key if this map contains a mapping for the key */
    public void remove(int key) {
        ListNode pre = findPre(table[hash(key)], key);
        if (pre == null || pre.next == null) {
            return;
        }
        pre.next = pre.next.next;
    }
    
    private boolean contains(int key) {
        ListNode pre = findPre(table[hash(key)], key);
        if (pre == null || pre.next == null) {
            return false;
        }
        return true;
    }
    
    private ListNode findPre(ListNode head, int key) { 
        //There is no node in the bucket
        if (head == null) {
            return null;
        }
       
        ListNode pre = head;
       
        while (pre.next != null && pre.next.key != key) {
            pre = pre.next;
        }
        return pre;
    }
    
    private int hash(int key) {
        //return key % bucket;
        return Integer.hashCode(key) % bucket;
    }
}

/**
 * Your MyHashMap object will be instantiated and called as such:
 * MyHashMap obj = new MyHashMap();
 * obj.put(key,value);
 * int param_2 = obj.get(key);
 * obj.remove(key);
 */


// class MyHashMap {
//     private class ListNode {
//         int key, val;
//         ListNode next;
//         ListNode (int key, int val) {
//             this.key = key;
//             this.val = val;
//         }
//     }
    
//     int bucket = 100000;
//     ListNode[] table;
//     /** Initialize your data structure here. */
//     public MyHashMap() {
//         table = new ListNode[bucket];
//         Arrays.fill(table, new ListNode(0,0));
//     }
    
//     /** value will always be non-negative. */
//     public void put(int key, int value) {
        
//         //update
//         ListNode pre = findPre(table[hash(key)], key);
//         if (pre.next != null) {
//             pre.next.key = key;
//             pre.next.val = value;
//         } 
//         else {
//             pre.next = new ListNode(key, value);
//         }
       
//     }
    
//     /** Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key */
//     public int get(int key) {
//         ListNode pre = findPre(table[hash(key)], key);
//         if (pre.next == null) {
//             return -1;
//         }
//         else {
//             return pre.next.val;
//         }
//     }
    
//     /** Removes the mapping of the specified value key if this map contains a mapping for the key */
//     public void remove(int key) {
//         ListNode pre = findPre(table[hash(key)], key);
//         if (pre.next == null) {
//             return;
//         }
//         pre.next = pre.next.next;
//     }
    
//     private boolean contains(int key) {
//         ListNode pre = findPre(table[hash(key)], key);
//         if (pre.next == null) {
//             return false;
//         }
//         return true;
//     }
    
//     private ListNode findPre(ListNode head, int key) {
//         ListNode pre = head;
//         while (pre.next != null && pre.next.key != key) {
//             pre = pre.next;
//         }
//         return pre;
//     }
    
//     private int hash(int key) {
//         //return key % bucket;
//         return Integer.hashCode(key) % bucket;
//     }
// }

/**
 * Your MyHashMap object will be instantiated and called as such:
 * MyHashMap obj = new MyHashMap();
 * obj.put(key,value);
 * int param_2 = obj.get(key);
 * obj.remove(key);
 */
```





## 217 [Contains Duplicate](https://leetcode.com/problems/contains-duplicate)    

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet();
        for (int element : nums) {
            if (!set.add(element)) {
                return true;
            }
        }
        return false;
    }
}
```







## 136 [Single Number](https://leetcode.com/problems/single-number)   

```java
class Solution {
    public int singleNumber(int[] nums) {
        Set<Integer> set = new HashSet();
        for (int element : nums) {
            if (!set.add(element)) {
                set.remove(element);
            }
        }
        return set.iterator().next();
    }
}
```





## 349 [Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays)    

```java
// class Solution {
    
//      public int[] intersection(int[] nums1, int[] nums2) {
//         if (nums1 == null || nums2 == null || nums1.length == 0 || nums2.length == 0) {
//             return new int[0];
//             // int[] result = {};
//             // return result;
//         }

//         Arrays.sort(nums2);
//         Set<Integer> set = new HashSet();
  
//         for (int i = 0; i < nums1.length; i++) {
//             int target = nums1[i];
//             if (binarySearch(nums2, target) != -1) {
//                 set.add(target);
//             }
//         }
        
//         int[] result = new int[set.size()];
//         // for (int i = 0; i < set.size(); i++) {
//         //     result[i] = set.get(i);
//         // }
//         int i = 0;
//         for (Integer val : set) {
//             result[i++] = val;
//         }
//         return result;
//     }
    
// //     public int[] intersection(int[] nums1, int[] nums2) {
// //         if (nums1 == null || nums2 == null || nums1.length == 0 || nums2.length == 0) {
// //             return new int[0];
// //             // int[] result = {};
// //             // return result;
// //         }
// //         Arrays.sort(nums1);
// //         Arrays.sort(nums2);
// //         ArrayList<Integer> list = new ArrayList();
// //         for (int i = 0; i < nums1.length; i++) {
// //             int target = nums1[i];
// //             if (i > 0 && target == nums1[i - 1]) {
// //                 continue;
// //             }
// //             if (binarySearch(nums2, target) != -1) {
// //                 list.add(target);
// //             }
// //         }
        
// //         int[] result = new int[list.size()];
// //         for (int i = 0; i < list.size(); i++) {
// //             result[i] = list.get(i);
// //         }
// //         return result;
// //     }
    
//     private int binarySearch(int[] array, int target) {
//         int left = 0, right = array.length - 1;
//         while (left <= right) {
//             int mid = left + (right - left) / 2;
//             if (array[mid] < target) {
//                 left = mid + 1;
//             }
//             else if (array[mid] > target) {
//                 right = mid - 1;
//             }
//             else {
//                 return mid;
//             }
//         }
//         return -1;
//     }
// }



// class Solution {
//      public int[] intersection(int[] nums1, int[] nums2) {
//         if (nums1 == null || nums2 == null || nums1.length == 0 || nums2.length == 0) {
//             return new int[0];
//             // int[] result = {};
//             // return result;
//         }
//         Set<Integer> set = new HashSet();
//         Set<Integer> interSet = new HashSet();
         
//         for (int i = 0; i < nums1.length; i++) {
//             set.add(nums1[i]);
//         }
//         for (int i = 0; i < nums2.length; i++) {
//             if (set.contains(nums2[i])) {
//                 interSet.add(nums2[i]);
//             }
//         }
        
//         int[] result = new int[interSet.size()];
         
//         int i = 0;
//         for (Integer val : interSet) {
//             result[i++] = val;
//         }
//         return result;
//     }
// }



class Solution {
     public int[] intersection(int[] nums1, int[] nums2) {
        if (nums1 == null || nums2 == null || nums1.length == 0 || nums2.length == 0) {
            return new int[0];
            // int[] result = {};
            // return result;
        }
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int i = 0;
        int j = 0;
         
         // use set
//         Set<Integer> set = new HashSet();
//         while (i < nums1.length && j < nums2.length) {
//             if (nums1[i] < nums2[j]) {
//                 i++;
//             }
//             else if (nums1[i] > nums2[j]) {
//                 j++;
//             }
//             else {
//                 set.add(nums1[i]);
//                 i++;
//                 j++;
//             }
//         }
        
//         int[] result = new int[set.size()];
//         int k = 0;
//         for (Integer val : set) {
//             result[k++] = val;
//         }
         
         
         
          // use list
        List<Integer> list = new ArrayList();
        while (i < nums1.length && j < nums2.length) {
            while (i > 0 && i < nums1.length && nums1[i] == nums1[i - 1]) {
                i++;
            }
            if (i == nums1.length) {
                break;
            }
            while (j > 0 && j < nums2.length && nums2[j] == nums2[j - 1]) {
                j++;
            }
            if (j == nums2.length) {
                break;
            }
      
            if (nums1[i] < nums2[j]) {
                i++;
            }
            else if (nums1[i] > nums2[j]) {
                j++;
            }
            else {
                list.add(nums1[i]);
                i++;
                j++;
            }
        }
        
        int[] result = new int[list.size()];
        int k = 0;
        for (Integer val : list) {
            result[k++] = val;
        }
        return result;
    }
}
```





### 202 [Happy Number](https://leetcode.com/problems/happy-number)   

```java
// class Solution {
//     public boolean isHappy(int n) {
        
//         Set<Integer> set = new HashSet();
//         set.add(n);
//         boolean isRepeat = false;
//         int pre = n;
//         while (isRepeat == false) {
//             int curr = getSquares(pre);
//             //System.out.println(curr);
//             if (curr == 1) {
//                 return true;
//             }
//             if (set.add(curr) == false) {
//                 isRepeat = true;
//             }
//             pre = curr;
//         }
//         return false;
//     }
    
//     private int getSquares(int n) {
//         int sum = 0;
//         while (n > 0) {
//             sum += (n % 10) * (n % 10);
//             n /= 10;
//         }
//         return sum;
//     }
// }



// class Solution {
//     Set<Integer> set = new HashSet();
    
//     public boolean isHappy(int n) {
//         if (n == 1) {
//             return true;
//         }
//         int curr = getSquares(n);
//         if (set.add(curr) == false) {
//             return false;
//         }
//         return isHappy(curr);
//     }
    
//     private int getSquares(int n) {
//         int sum = 0;
//         while (n > 0) {
//             sum += (n % 10) * (n % 10);
//             n /= 10;
//         }
//         return sum;
//     }
// }


// class Solution {
//     public boolean isHappy(int n) {
//         Set<Integer> set = new HashSet();
//         return helper(n, set);
//     }
    
//     private boolean helper(int n, Set<Integer> set) {
//         if (n == 1) {
//             return true;
//         }
//         int curr = getSquares(n);
//         if (set.add(curr) == false) {
//             return false;
//         }
//         return helper(curr, set);
//     }
    
//     private int getSquares(int n) {
//         int sum = 0;
//         while (n > 0) {
//             sum += (n % 10) * (n % 10);
//             n /= 10;
//         }
//         return sum;
//     }
// }



class Solution {
    public boolean isHappy(int n) {
        int slow = n, fast = n;
        do {
            slow = getSquares(slow);
            fast = getSquares(getSquares(fast));
        } while (slow != fast);
        return slow != 1 ? false : true;
    }
    
    private int getSquares(int n) {
        int sum = 0;
        int temp;
        while (n > 0) {
            temp = n % 10;
            sum += temp * temp;
            n /= 10;
        }
        return sum;
    }
}
```





## 1  [Two Sum](https://leetcode.com/problems/two-sum)    

```java
// class Solution {
//     public int[] twoSum(int[] nums, int target) {
//         Map<Integer, Integer> map = new HashMap();
//         int[] res = new int[2];
        
//         for (int i = 0; i < nums.length; i++) {
//             if (map.containsKey(target - nums[i])) {
//                 return new int[] {map.get(target - nums[i]), i};
//             }
//             map.put(nums[i], i);
//         }
//         return null;
//         //throw new IllegalArgumentException("No two sum solution");
//     }
// }


// wrong ============> sort break the indice
// class Solution {
//     public int[] twoSum(int[] nums, int target) {
//         if (nums == null || nums.length < 2) {
//             return null;
//         }
        
//         Arrays.sort(nums);
//         int left = 0;
//         int right = nums.length - 1;
//         while (left < right) {
//             int sum = nums[left] + nums[right];
            
//             if (sum < target) {
//                 left++;
//             }
//             else if (sum > target){
//                 right--;
//             }
//             else {
//                 return new int[] {left, right};
//             }
//         }
//         return null;
   
//     }
// }


class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap(); // value => indice
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i])) {
                return new int[] {map.get(target - nums[i]), i};
            }
            map.put(nums[i], i);
        }
        //return new int[] {-1, -1};
        //throw new IllegalArgumentException("No two sum solution");
        return null;
    }
}
```







## 205  [Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings)   

```java
// class Solution {
//     public boolean isIsomorphic(String s, String t) {
//         Map<Character, List<Integer>> sMap = getMap(s);
//         Map<Character, List<Integer>> tMap = getMap(t);
        
//         Set<Character> set = new HashSet();
//         for (int i = 0; i < s.length(); i++) {
//             if (set.contains(s.charAt(i))) {
//                 continue;
//             }
//             set.add(s.charAt(i));
//             List<Integer> sList = sMap.get(s.charAt(i));
//             List<Integer> tList = tMap.get(t.charAt(i));
//             if (!sList.equals(tList)) {
//                 return false;
//             }
//         }
//         return true;
//     }
    
//     private Map<Character, List<Integer>> getMap (String s) {
//         Map<Character, List<Integer>> sMap = new HashMap();
//         for (int i = 0; i < s.length(); i++) {
//             if (!sMap.containsKey(s.charAt(i))) {
//                 List<Integer> list = new ArrayList();
//                 list.add(i);
//                 sMap.put(s.charAt(i), list);
//             }
//             else {
//                 sMap.get(s.charAt(i)).add(i);
//             }
//         }
        
//         for (Map.Entry<Character, List<Integer>> entry : sMap.entrySet()) {
//             System.out.println(entry.getKey());
//             System.out.println(entry.getValue());
//         }
//         return sMap;
//     }
// }




// class Solution {
//     public boolean isIsomorphic(String s, String t) {
//         Map<Character, Integer> sMap = new HashMap();
//         Map<Character, Integer> tMap = new HashMap();
//         for (int i = 0; i < s.length(); i++) {
//             Integer sIn = sMap.get(s.charAt(i));
//             Integer tIn = tMap.get(t.charAt(i));
//             if (sIn == null && tIn == null) {
//                 sMap.put(s.charAt(i), i);
//                 tMap.put(t.charAt(i), i);
//             }
//             //else if (sIn == null || tIn == null || !sIn.equals(tIn)) {
//             else if (sIn == null || tIn == null || !sIn.equals(tIn)) {
//                 return false;
//             }
//             else {
//                 sMap.put(s.charAt(i), i);
//                 tMap.put(t.charAt(i), i);
//             }
//         }
//         return true;
//     }
// }



//-------------------------------------why one case can not pass?   Integer => null == equal
// class Solution {
//     public boolean isIsomorphic(String s, String t) {
//         Map<Character, Integer> sMap = new HashMap();
//         Map<Character, Integer> tMap = new HashMap();
//         for (int i = 0; i < s.length(); i++) {
//             Integer sIn = sMap.get(s.charAt(i));
//             Integer tIn = tMap.get(t.charAt(i));
//             if (sIn == null && tIn == null) {
//                 sMap.put(s.charAt(i), i);
//                 tMap.put(t.charAt(i), i);
//             }
//             else if (sIn == null || tIn == null || !sIn.equals(tIn)) {
//             // why 128 != 128 => true ?
//             //else if (sIn == null || tIn == null || sIn != tIn) { 
//                 // System.out.println(sIn);
//                 // System.out.println(tIn);
//                 // System.out.println(sIn != tIn);
//                 // System.out.println(!sIn.equals(tIn));
//                 return false;
//             }
//             else {
//                 sMap.put(s.charAt(i), i);
//                 tMap.put(t.charAt(i), i);
//             }
//         }
        
        
//         //wrong
//         // for (int i = 0; i < s.length(); i++) {
//         //     Integer sIn = sMap.get(s.charAt(i));
//         //     Integer tIn = tMap.get(t.charAt(i));
//         //     if (sIn != tIn) {
//         //         System.out.println(sIn);
//         //         System.out.println(tIn);
//         //         System.out.println(sIn == tIn);
//         //         System.out.print(sIn.equals(tIn));
//         //         return false;
//         //     }
//         //     sMap.put(s.charAt(i), i);
//         //     tMap.put(t.charAt(i), i);
//         // }
        
//         return true;
//     }
// }




// class Solution {
//     public boolean isIsomorphic(String s, String t) {
//         Map<Character, Integer> sMap = new HashMap();
//         Map<Character, Integer> tMap = new HashMap();
//         for (int i = 0; i < s.length(); i++) {
//             if (sMap.containsKey(s.charAt(i)) == false && tMap.containsKey(t.charAt(i)) == false) {
//                 sMap.put(s.charAt(i), i);
//                 tMap.put(t.charAt(i), i);
//             }
//             else if (sMap.containsKey(s.charAt(i)) == false || tMap.containsKey(t.charAt(i)) == false) {
//                 return false;
//             }
//             else {
//                 Integer sIn = sMap.get(s.charAt(i));
//                 Integer tIn = tMap.get(t.charAt(i));
                
//                 // == vs equals
//                 //if (sIn != tIn) {
//                 if (!sIn.equals(tIn)) {
//                     // System.out.println(sIn);
//                     // System.out.println(tIn);
//                     // System.out.println(sIn != tIn);
//                     // System.out.println(!sIn.equals(tIn));
//                     return false;
//                 }
//                 else {
//                     sMap.put(s.charAt(i), i);
//                     tMap.put(t.charAt(i), i);
//                 }
//             }

            
//             //else if (sIn == null || tIn == null || !sIn.equals(tIn)) {
//             // why 128 != 128 => true ?
//             //else if (sIn == null || tIn == null || sIn != tIn) { 

//         }
//         return true;
//     }
// }




// containsValue O(n) n is the size of hashtable, but there are only 128 chars!!!! 128 pair at most so n <= 128
public class Solution {
    public boolean isIsomorphic(String s, String t) {
        HashMap<Character, Character> map = new HashMap<Character, Character>();
        for (int i = 0; i < s.length(); i++) {
            char a = s.charAt(i);
            char b = t.charAt(i);
            if (map.containsKey(a)) {
                if (map.get(a) != b) {
                    return false;
                }
                else {
                    continue;
                }
            }
            else {
                // containsValue O(n) n is the size of hashtable, but there are only 128 chars!!!! 128 pair at most so n <= 128
                if (map.containsValue(b)) {
                    return false;
                }
                else {
                    map.put(a, b);
                }
            }
        }
        return true;
    }
}





// class Solution {
//     public boolean isIsomorphic(String s, String t) {
//         int[] sArray = new int[128];
//         int[] tArray = new int[128];
     
//         for (int i = 0; i < s.length(); i++) {
//             if (sArray[s.charAt(i)] != tArray[t.charAt(i)]) {
//                 return false;
//             }
//             //include 0 = 0, happen for the first time
//             sArray[s.charAt(i)] = i + 1; // char => int
//             tArray[t.charAt(i)] = i + 1; // char => int
//         }
//         return true;
//     }
// }


// class Solution {
//     public boolean isIsomorphic(String s, String t) {
//         char[] sArray = new char[128];
//         char[] tArray = new char[128];
//         for (int i = 0; i < s.length(); i++) {
//             if (sArray[s.charAt(i)] == 0 && tArray[t.charAt(i)] == 0) {
//                 sArray[s.charAt(i)] = t.charAt(i);
//                 tArray[t.charAt(i)] = s.charAt(i);
//             } else {
//                 // null can not be used for ==
//                 if (sArray[s.charAt(i)] != t.charAt(i) || tArray[t.charAt(i)] != s.charAt(i)) {
//                     return false;
//                 }
//             }
//             //include null = null, happen for the first time
//         }
//         return true;
//     }
// }


//diff between char[] and character[]  
//[0,0,0.....0] VS [null, null, null.....]
//null can not be used for ==

// class Solution {
//     public boolean isIsomorphic(String s, String t) {
//         Map<Character, Character> sMap = new HashMap();
//         Map<Character, Character> tMap = new HashMap();
//         for (int i = 0; i < s.length(); i++) {
//             if (sMap.get(s.charAt(i)) == null && tMap.get(t.charAt(i)) == null) {
//                 sMap.put(s.charAt(i), t.charAt(i));
//                 tMap.put(t.charAt(i), s.charAt(i));
//             } else {
//                 Character sChar = sMap.get(s.charAt(i));
//                 Character tChar = tMap.get(t.charAt(i));
//                 // null can not be used for ==
//                 if (sChar == null || tChar == null || sChar != t.charAt(i) || tChar != s.charAt(i)) {
//                     return false;
//                 }
//             }
        
//             //include null = null, happen for the first time
//         }
//         return true;
//     }
// }
```





599 [Minimum Index Sum of Two Lists](https://leetcode.com/problems/minimum-index-sum-of-two-lists)    

```java
class Solution {
    public String[] findRestaurant(String[] list1, String[] list2) {
        ArrayList<String> res = new ArrayList();
        int sum = Integer.MAX_VALUE;
        HashMap<String, Integer> map = new HashMap();
        
        for (int i = 0; i < list1.length; i++) {
            map.put(list1[i], i);
        }
        
        for (int i = 0; i < list2.length; i++) {
            if (map.containsKey(list2[i])) {
                if (map.get(list2[i]) + i < sum) {
                    sum = map.get(list2[i]) + i;
                    res.clear();
                    res.add(list2[i]);
                }
                else if (map.get(list2[i]) + i == sum) {
                    res.add(list2[i]);
                }
            }
        }
        
        return res.toArray(new String[res.size()]); // => String[]
        //return res.toArray(); => object[]
    }
}
```



## 387 [First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string)   

```java

// class Solution {
//     public int firstUniqChar(String s) {
//         Map<Character, int[]> map = new HashMap();
//         for (int i = 0; i < s.length(); i++) {
//             if (map.containsKey(s.charAt(i))) {
//                 map.get(s.charAt(i))[0]++; //right map.get(s.charAt(i)) => array[] => can be changed!!!! reference
//                 //map.put(s.charAt(i), map.get(s.charAt(i)) + 1);
//             }
//             else {
//                 map.put(s.charAt(i), new int[] {1, i});
//             }
//         }
        
//         for (int i = 0; i < s.length(); i++) {
//             if (map.get(s.charAt(i))[0] == 1) {
//                 return map.get(s.charAt(i))[1];
//             }
//         }
        
//         //hashMap non-order!!!!!!!!
//         // for (Map.Entry<Character, int[]> entry: map.entrySet()) {
//         //     if (entry.getValue()[0] == 1) {
//         //         return entry.getValue()[1];
//         //     }
//         // }
//         return -1;
//     }
// }



// class Solution {
//     public int firstUniqChar(String s) {
//         Map<Character, Integer> map = new HashMap();
//         for (int i = 0; i < s.length(); i++) {
//             // if (map.containsKey(s.charAt(i))) {
//             //     //System.out.print(map.get(s.charAt(i)));
//             //     //Wrong get => Integer => can not be changed !!!!!
//             //     //map.get(s.charAt(i)) = map.get(s.charAt(i)) + 1;
//             //     map.put(s.charAt(i), map.get(s.charAt(i)) + 1);
//             // }
//             // else {
//             //     map.put(s.charAt(i), 1);
//             // }
//             map.put(s.charAt(i), map.getOrDefault(s.charAt(i), 0) + 1);
//         }
 
        
//         for (int i = 0; i < s.length(); i++) {
//             if (map.get(s.charAt(i)) == 1) {
//                 return i;
//             }
//         }
        

//         return -1;
//     }
// }



class Solution {
    public int firstUniqChar(String s) {
        int[] map = new int[128];
        for (int i = 0; i < s.length(); i++) {
            map[s.charAt(i)]++;
        }
 
        for (int i = 0; i < s.length(); i++) {
            if (map[s.charAt(i)] == 1) {
                return i;
            }
        }

        return -1;
    }
}
```





## 350 [Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii)    

```java
// class Solution {
//     public int[] intersect(int[] nums1, int[] nums2) {
//         if (nums1 == null || nums2 == null || nums1.length == 0 || nums2.length == 0) {
//             return new int[0];
//         }
//         Arrays.sort(nums1);
//         Arrays.sort(nums2);
//         int p1 = 0;
//         int p2 = 0;
//         ArrayList<Integer> list = new ArrayList();
//         while (p1 < nums1.length && p2 < nums2.length) {
//             if (nums1[p1] < nums2[p2]) {
//                 p1++;
//             }
//             else if (nums1[p1] > nums2[p2]) {
//                 p2++;
//             }
//             else {
//                 list.add(nums1[p1]);
//                 p1++;
//                 p2++;
//             }
//         }
//         int[] result = new int[list.size()];
        
//         int i = 0;
//         for (Integer val : list) {
//             result[i++] = val;
//         }
//         return result;
//     }
// }

// class Solution {
//     public int[] intersect(int[] nums1, int[] nums2) {
//         List<Integer> res = new ArrayList();
//         Map<Integer, Integer> map1 = getMap(nums1);
//         Map<Integer, Integer> map2 = getMap(nums2);
//         for (Map.Entry<Integer, Integer> entry: map1.entrySet()) {
//             if (map2.containsKey(entry.getKey())) {
//                 int times = Math.min(map1.get(entry.getKey()), map2.get(entry.getKey()));
//                 for (int i = 0; i < times; i++) {
//                     res.add(entry.getKey());
//                 }
//             }
//         }
        
//         int[] array = new int[res.size()];
//         int i = 0;
//         for (int element : res) {
//             array[i++] = element;
//         }
//         return array;
//         //return res.toArray(new int[res.size()]);
//     }
    
//     private Map<Integer, Integer> getMap(int[] nums) {
//         Map<Integer, Integer> map = new HashMap();
//         for (int element : nums) {
//             map.put(element, map.getOrDefault(element, 0) + 1);
//         }
//         return map;
//     }
// }


class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        List<Integer> res = new ArrayList();
        Map<Integer, Integer> map = getMap(nums1);
        for (int i = 0; i < nums2.length; i++) {
            if (map.containsKey(nums2[i]) && map.get(nums2[i]) > 0) {
                map.put(nums2[i], map.get(nums2[i]) - 1);
                res.add(nums2[i]);
            }
        }
        
        int[] array = new int[res.size()];
        int i = 0;
        for (int element : res) {
            array[i++] = element;
        }
        return array;
        //return res.toArray(new int[res.size()]);
    }
    
    private Map<Integer, Integer> getMap(int[] nums) {
        Map<Integer, Integer> map = new HashMap();
        for (int element : nums) {
            map.put(element, map.getOrDefault(element, 0) + 1);
        }
        return map;
    }
}
```







## 219 [Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii)   

```java
// class Solution {
//     public boolean containsNearbyDuplicate(int[] nums, int k) {
//         if (k <= 0 || nums == null || nums.length < 2) {
//             return false;
//         }
        
//         Map<Integer, int[]> map = new HashMap();
//         boolean res = false;
//         for (int i = 0; i < nums.length; i++) {
//             if (!map.containsKey(nums[i])) {
//                 map.put(nums[i], new int[] {i, i});
//             }
//             else {
//                 int diff1 = map.get(nums[i])[1] - map.get(nums[i])[0];
//                 int diff2 = i - map.get(nums[i])[1];
//                 //pay attention to diff1 == 0 
//                 //pay attention to ==
//                 //[1,2,1,3,1,1] k = 1    without == => false
//                 if (diff1 == 0 || diff2 <= diff1) {
//                     map.get(nums[i])[0] = map.get(nums[i])[1];
//                     map.get(nums[i])[1] = i;
//                 }
//                 System.out.println("num" + nums[i] + " min: " + map.get(nums[i])[0] + " max: " + map.get(nums[i])[1]);
//             }
//         }
        
//         for (Map.Entry<Integer, int[]> entry : map.entrySet()) {
//             int diff = entry.getValue()[1] - entry.getValue()[0];
//             // diff > 0!!!!!
//             if (diff <= k && diff > 0) {
//                 return true;
//             }
//         }
//         return false;
//     }
// }


class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        if (k <= 0 || nums == null || nums.length < 2) {
            return false;
        }
        
        Map<Integer, Integer> map = new HashMap();
        for (int i = 0; i < nums.length; i++) {
        //the previous value associated with key, or null if there was no mapping for key. (A null return can also indicate that the map previously associated null with key, if the implementation supports null values.)
            Integer pre = map.put(nums[i], i); 
            if (pre != null && i - pre <= k) {
                return true;
            }
        }
        // for (int i = 0; i < nums.length; i++) {
        //     if (map.containsKey(nums[i]) && i - map.get(nums[i]) <= k) {
        //         return true;
        //     }
        //     map.put(nums[i], i);
        // }
        return false;
    }
}




// class Solution {
//     public boolean containsNearbyDuplicate(int[] nums, int k) {
//         if (k <= 0 || nums == null || nums.length < 2) {
//             return false;
//         }
//         //wrong => maybe all elements are unique, so there are no duplicate
//         // if (k >= nums.length - 1) {
//         //     return true;
//         // }
        
//         Set<Integer> set = new HashSet();
//         for (int i = 0; i < Math.min(k + 1, nums.length); i++) {
//             if (set.add(nums[i]) == false) {
//                 return true;
//             }
//         }
        
//         for (int i = k + 1; i < nums.length; i++) {
//             set.remove(nums[i - (k + 1)]);
//             if (set.add(nums[i]) == false) {
//                 return true;
//             }
//         }
        
//         // for (int i = 0; i < nums.length; i++) {
//         //     if (i <= k) {
//         //         if (set.add(nums[i]) == false) {
//         //             return true;
//         //         }
//         //     }
//         //     else {
//         //         set.remove(nums[i - (k + 1)]);
//         //         if (set.add(nums[i]) == false) {
//         //             return true;
//         //         }
//         //     }
//         // }
        
//         return false;
//     }
// }




// class Solution {
//     public boolean containsNearbyDuplicate(int[] nums, int k) {
//         if (k <= 0 || nums == null || nums.length < 2) {
//             return false;
//         }
        
//         // k sliding window 
//         Set<Integer> set = new HashSet();
//         for (int i = 0; i < nums.length; i++) {
//             if (set.add(nums[i]) == false) { // set.size() <= k
//                 return true;
//             }
//             if (set.size() > k) { // remove the smallest indice set
//                 set.remove(nums[i - k]);
//             }
//         }
//         return false;
//     }
// }
```





##  359 [Logger Rate Limiter](https://leetcode.com/problems/logger-rate-limiter)    

```java
class Logger {
    Map<String, Integer> map;
    /** Initialize your data structure here. */
    public Logger() {
        map = new HashMap();
    }
    
    /** Returns true if the message should be printed in the given timestamp, otherwise returns false.
        If this method returns false, the message will not be printed.
        The timestamp is in seconds granularity. */
    public boolean shouldPrintMessage(int timestamp, String message) {
        // if (map.containsKey(message) == false) {
        //     map.put(message, timestamp);
        //     return true;
        // }
        // if (timestamp - map.get(message) >= 10) {
        //     map.put(message, timestamp);
        //     return true;
        // }
        //return false;
        
        if (timestamp >= map.getOrDefault(message, 0)) {
            map.put(message, timestamp + 10);
            return true;
        }
        return false;
    }
}

/**
 * Your Logger object will be instantiated and called as such:
 * Logger obj = new Logger();
 * boolean param_1 = obj.shouldPrintMessage(timestamp,message);
 */
```





## 49 [Group Anagrams](https://leetcode.com/problems/group-anagrams)    

```java
// O(Nlog(N))
// class Solution {
//     public List<List<String>> groupAnagrams(String[] strs) {
//         Map<String, List<String>> map = new HashMap();
//         for (String element : strs) {
//             //sort a string 
//             char[] charArray = element.toCharArray();
//             Arrays.sort(charArray);
//             //String key = new String(charArray);
//             String key = String.valueOf(charArray);
            
//             // if (map.containsKey(key) == false) {
//             //     List<String> list = new ArrayList();
//             //     list.add(element);
//             //     map.put(key, list);
//             // }
//             // else {
//             //     map.get(key).add(element);
//             // }
            
            
            
//             // way 2
//             // if (map.containsKey(key) == false) {
//             //     map.put(key, new ArrayList());
//             // }
//             // map.get(key).add(element);
            
            
//             // way 3
//             List<String> list = map.getOrDefault(key, new ArrayList());
//             list.add(element);
//             map.put(key, list);
            
//         }
        
//         List<List<String>> res = new ArrayList();
//         for (Map.Entry<String, List<String>> entry : map.entrySet()) {
//             res.add(entry.getValue());
//         }
//         return res;
//     }
// }



//without sort O(NK)
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap();
        for (String element : strs) {
            int[] charArray = new int[26];
            for (int i = 0; i < element.length(); i++) {
                charArray[element.charAt(i) - 'a']++;
            }
            
            StringBuilder sb = new StringBuilder();
            for (int num : charArray) {
                sb.append("#");
                sb.append(num);
            }
            
            String key = sb.toString();
            //System.out.println(element +  "---x---" + key);
            if (map.containsKey(key) == false) {
                map.put(key, new ArrayList());
            }
            map.get(key).add(element);
        }
        
        List<List<String>> res = new ArrayList();
        for (Map.Entry<String, List<String>> entry : map.entrySet()) {
            res.add(entry.getValue());
        }
        return res;
    }
}
```







## 249[Group Shifted Strings](https://leetcode.com/problems/group-shifted-strings)    

```java
// class Solution {
//     public List<List<String>> groupStrings(String[] strings) {
//         Map<Set<String>, List<String>> map = new HashMap();
        
//         for (String element : strings) {
//             checkAndUpdate(map, element);
//         }
        
//     }
    
//     private String getCode(String element) {
//         int[] charArray = element.toCharArray();
//         for (int i = 0; i < strings.length(); i++) {
//             charArrays[strings.charAt(i) - 'a']++;
//         }

//         StringBuilder sb = new StringBuilder();
//         for (int num : charArray) {
//             sb.append("#");
//             sb.append(num);
//         }
//         String code = sb.toString();
//         return code;
//     }
    
//     private void checkAndUpdate(Map<Set<String>, List<String>> map, String element) {
//         String code = getCode(element);
//         for (Map.Entry<Set<String>, List<String>> entry : map.entrySet()) {
//             if (entry.getKey().contains(code)) {
//                 entry.getValue().add(element);
//                 return;
//             }
//         }
//         addNewSet(map, element);
//     }
    
//     private void addNewSet(Map<Set<String>, List<String>> map, String element) {
//         //???? how 
//     }
// }



class Solution {
    public List<List<String>> groupStrings(String[] strings) {
        Map<String, List<String>> map = new HashMap();
        
        for (String element : strings) {
            int offset = element.charAt(0) - 'a';
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < element.length(); i++) {
                char c = (char) (element.charAt(i) - offset);
                if (c < 'a') {
                    c += 26;
                }
                sb.append(c);
            }
            String key = sb.toString();
            
            if (map.containsKey(key) == false) {
                map.put(key, new ArrayList());
            }
            map.get(key).add(element);
        }
        
        List<List<String>> res = new ArrayList();
        for (Map.Entry<String, List<String>> entry : map.entrySet()) {
            res.add(entry.getValue());
        }
        return res;
    }
}
```



## 36 [Valid Sudoku](https://leetcode.com/problems/valid-sudoku)   

```java
// class Solution {
//     public boolean isValidSudoku(char[][] board) {
//         int line = board.length;
//         int column = board[0].length;
        
//         Map<Integer, Set<Character>> map = new HashMap();
        
//         //line 0-8
//         for (int i = 0; i < line; i++) {
//             for (int j = 0; j < column; j++) {
//                 char c = board[i][j];
//                 if (c != '.') {
//                     if (map.containsKey(i) == false) {
//                         map.put(i, new HashSet());
//                     } 
//                     if (map.get(i).add(c) == false) {
//                         return false;
//                     }
//                 }
//             }
//         }
        
//         map.clear();
        
//         //column 0-8
//         for (int j = 0; j < column; j++) {
//             for (int i = 0; i < line; i++) {
//                 char c = board[i][j];
//                 if (c != '.') {
//                     if (map.containsKey(j) == false) {
//                         map.put(j, new HashSet());
//                     } 
//                     if (map.get(j).add(c) == false) {
//                         return false;
//                     }
//                 }
//             }
//         }

        
//         map.clear();
        
//         //box 0-8
//         for (int k = 0; k < 9; k++) {
//             for (int i = k / 3 * 3; i < k / 3 * 3 + 3; i++) {
//                 for (int j = k % 3 * 3; j < k % 3 * 3 + 3; j++) {
//                     char c = board[i][j];
//                     if (c != '.') {
//                         if (map.containsKey(k) == false) {
//                             map.put(k, new HashSet());
//                         }
//                         if (map.get(k).add(c) == false) {
//                             return false;
//                         }
//                     }
//                 }
//             }
//         }
//         return true;
//     }
// }


// class Solution {
//     public boolean isValidSudoku(char[][] board) {
//         int line = board.length;
//         int column = board[0].length;
        
//         Set<Character> set = new HashSet();
        
//         //line 0-8
//         for (int i = 0; i < line; i++) {
//             for (int j = 0; j < column; j++) {
//                 char c = board[i][j];
//                 if (c != '.') {
//                     if (set.add(c) == false) {
//                         return false;
//                     }
//                 }
//             }
//             set.clear();
//         }
        
        
//         //column 0-8
//         for (int j = 0; j < column; j++) {
//             for (int i = 0; i < line; i++) {
//                 char c = board[i][j];
//                 if (c != '.') {
//                     if (set.add(c) == false) {
//                         return false;
//                     }
//                 }
//             }
//             set.clear();
//         }
        
//         //box 0-8
//         for (int k = 0; k < 9; k++) {
//             for (int i = k / 3 * 3; i < k / 3 * 3 + 3; i++) {
//                 for (int j = k % 3 * 3; j < k % 3 * 3 + 3; j++) {
//                     char c = board[i][j];
//                     if (c != '.') {
//                         if (set.add(c) == false) {
//                             return false;
//                         }
//                     }
//                 }
//             }
//             set.clear();
//         }
//         return true;
//     }
// }



class Solution {
    public boolean isValidSudoku(char[][] board) {
        int line = board.length;
        int column = board[0].length;
        
        Map<Integer, Set<Character>> map = new HashMap();
        
        //line 0-8
        for (int i = 0; i < line; i++) {
            for (int j = 0; j < column; j++) {
                char c = board[i][j];
                if (c != '.') {
                    //System.out.println("i:" + i + "j:" + j);
                    for (int key : getKeys(i, j)) {
                        //System.out.println("key" + key);
                        if (map.containsKey(key) == false) {
                            map.put(key, new HashSet());
                        }
                        if (map.get(key).add(c) == false) {
                            //System.out.println("key:" + key);
                            //System.out.println(c);
                            return false;
                        }
                    }
                }
            }
        }
        return true;
    }
    
    private int[] getKeys (int i, int j) {
        //return new int[] {i, j + 9, i / 3 + j / 3 * 3 + 18}; // 0 3 6 1 4 7 2 5 8 col => 0 1 2 3 4 5 6 7 8 9
        return new int[] {i, j + 9, i / 3 * 3 + j / 3 + 18}; // 0 1 2 3 4 5 6 7 8 
    }
}


//O(3n*n) Space O(3n*n)
// class Solution {
//     public boolean isValidSudoku(char[][] board) {
//         int line = board.length;
//         int column = board[0].length;
        
//         Set<String> set = new HashSet();
        
//         for (int i = 0; i < line; i++) {
//             for (int j = 0; j < column; j++) {
//                 char c = board[i][j];
//                 if (c != '.') {
//                     //System.out.println("i:" + i + "j:" + j);
//                     for (String key : getKeys(i, j, c)) {
//                         //System.out.println(key);
//                         if (set.add(key) == false) {
//                             return false;
//                         }
//                     }
//                 }
//             }
//         }
//         return true;
//     }
    
//     private String[] getKeys (int i, int j, char c) {
//         return new String[] {
//             c + "-row:" + i, 
//             c + "-col:" + j,
//             c + "-cubeRow:" + i / 3 + "-cubeCol:" + j / 3
//         };
//     }
// }



//O(3n*n) Space O(3n*n)
// class Solution {
//     public boolean isValidSudoku(char[][] board) {
//         int line = board.length;
//         int column = board[0].length;
        
        
        
//         for (int i = 0; i < line; i++) {
//             Set<Character> row = new HashSet();
//             Set<Character> col = new HashSet();
//             Set<Character> cube = new HashSet();
            
//             for (int j = 0; j < column; j++) {
//                 if (board[i][j] != '.' && row.add(board[i][j]) == false) {
//                     return false;
//                 }
//                 if (board[j][i] != '.' && col.add(board[j][i]) == false) {
//                     return false;
//                 }
//                 int rowOffset = i / 3 * 3;
//                 int colOffset = i % 3 * 3;
//                 if (board[rowOffset + j / 3][colOffset + j % 3] != '.' && cube.add(board[rowOffset + j / 3][colOffset + j % 3]) == false) {
//                     return false;
//                 }
//             }
//         }
//         return true;
//     }
// }


//O(3n*n) Space O(3n*n)
// class Solution {
//     public boolean isValidSudoku(char[][] board) {
//         int line = board.length;
//         int column = board[0].length;
//         int[][] row = new int[9][9];
//         int[][] col = new int[9][9];
//         int[][] cube = new int[9][9];
        
        
//         for (int i = 0; i < line; i++) {
//             for (int j = 0; j < column; j++) {
//                 if (board[i][j] == '.') {
//                     continue;
//                 }
//                 int num = board[i][j] - '0' - 1;
//                 int k = i / 3 * 3 + j / 3;

//                 if (row[i][num] != 0 ||  col[j][num] != 0 || cube[k][num] != 0) {
//                     return false;
//                 }
//                 row[i][num] = col[j][num] = cube[k][num] = 1;
//             }
//         }
//         return true;
//     }
// }


```





## 652 [Find Duplicate Subtrees](https://leetcode.com/problems/find-duplicate-subtrees)    

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
    
    public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
        Map<String, Integer> map = new HashMap();
        List<TreeNode> res = new ArrayList();
        preDfs(root, map, res);
        return res;
    }
    
    private String preDfs(TreeNode root, Map<String, Integer> map, List<TreeNode> res) {
        if (root == null) {
            return "#";
        }
        String serial = root.val + "," + preDfs(root.left, map, res) + "," + preDfs(root.right, map, res);
        //System.out.println(serial);
        map.put(serial, map.getOrDefault(serial, 0) + 1);
        if (map.get(serial) == 2) {
            res.add(root);
        }
        return serial;
    }
}
```





## 771 [Jewels and Stones](https://leetcode.com/problems/jewels-and-stones) 

```java
class Solution {
    public int numJewelsInStones(String J, String S) {
        Set<Character> set = new HashSet();
        for (int i = 0; i < J.length(); i++) {
            set.add(J.charAt(i));
        }
        int res = 0;
        for (int i = 0; i < S.length(); i++) {
            if (set.contains(S.charAt(i))) {
                res++;
            }
        }
        return res;
    }
}
```



## 3 [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters)   

```java
// class Solution {
//     public int lengthOfLongestSubstring(String s) {
//         Set<Character> set = new HashSet();
//         int res = 0, slow = 0, fast = 0;
//         while (fast < s.length()) {
//             if (set.contains(s.charAt(fast)) == false) {
//                 set.add(s.charAt(fast));
//                 // System.out.println("fast:" + fast);
//                 // System.out.println("slow:" + slow);
                
//                 //res = Math.max(res, fast - slow + 1);
                
//                 res = Math.max(res, set.size());
//                 fast++;
//             }
//             else {
//                 set.remove(s.charAt(slow));
//                 slow++;
//             }
//         }
    
//         return res;
//     }
// }


// class Solution {
//     public int lengthOfLongestSubstring(String s) {
//         Map<Character, Integer> map = new HashMap();
//         int res = 0, slow = 0, fast = 0;
        
//         while (fast < s.length()) {
//             if (map.containsKey(s.charAt(fast)) == true) {
//                 // Pay attention to Math.max  "abba"  slow = >2 , s.charAt('a')=>0 without Math.max , slow ==> 0 + 1
//                 slow = Math.max(slow, map.get(s.charAt(fast)) + 1); 
//                 //System.out.println("slow" + slow);
//             }
//             res = Math.max(res, fast - slow + 1);
//             map.put(s.charAt(fast), fast);
//             fast++;
//         }
    
//         return res;
//     }
// }


class Solution {
    public int lengthOfLongestSubstring(String s) {
        int[] charArray = new int[128];
        int res = 0, slow = 0, fast = 0;
        Arrays.fill(charArray, -1); // in case string only with 1 character
        
        while (fast < s.length()) {
            // can not put into if != 0, maybe charArray[s.charAt(fast)] == 0!!!!!!!
            // Pay attention to Math.max  "abba"  slow = >2 , s.charAt('a')=>0 without Math.max , slow ==> 0 + 1
            
            // if (charArray[s.charAt(fast)] != -1) {
            //     slow = Math.max(slow, charArray[s.charAt(fast)] + 1); 
            // }
            
            // charArray[s.charAt(fast)]  == -1 will not affect slow!!!
            slow = Math.max(slow, charArray[s.charAt(fast)] + 1); 
            res = Math.max(res, fast - slow + 1);
            charArray[s.charAt(fast)] = fast;
            fast++;
        }
    
        return res;
    }
}



// class Solution {
//     public int lengthOfLongestSubstring(String s) {
//         int[] charArray = new int[128];
//         int res = 0, slow = 0, fast = 0;
        
//         while (fast < s.length()) {
//             // if (charArray[s.charAt(fast)] != 0) {
//             //     // Pay attention to Math.max  "abba"  slow = >2 , s.charAt('a')=>0 without Math.max , slow ==> 0 + 1
//             //     slow = Math.max(slow, charArray[s.charAt(fast)]); 
//             // }
            
//             //charArray[s.charAt(fast)] == 0 will not affect slow!
//             slow = Math.max(slow, charArray[s.charAt(fast)]); 
//             res = Math.max(res, fast - slow + 1);
//             charArray[s.charAt(fast)] = fast + 1;
//             fast++;
//         }
//         return res;
//     }
// }
```





## 170 [Two Sum III - Data structure design](https://leetcode.com/problems/two-sum-iii-data-structure-design)    

```java
// class TwoSum {
//     Map<Integer, List<Integer>> map;
//     int i = 0;
    
//     /** Initialize your data structure here. */
//     public TwoSum() {
//         map = new HashMap();
//     }
    
//     /** Add the number to an internal data structure.. */
//     public void add(int number) {
//         if (map.containsKey(number) == false) {
//             map.put(number, new ArrayList());
//         }
//         map.get(number).add(i++);
//     }
    
    
//     /** Find if there exists any pair of numbers which sum is equal to the value. */
//     public boolean find(int value) {
//         for (Map.Entry<Integer, List<Integer>> entry : map.entrySet()) {
//             if (map.containsKey(value - entry.getKey())) {
//                 // if (value == 2 * entry.getKey()) {
//                 //     if (entry.getValue().size() > 1) {
//                 //         return true;
//                 //     }
//                 // }
//                 // else {
//                 //     return true;
//                 // }
                
      
//                 if (value != 2 * entry.getKey() || map.get(entry.getKey()).size() > 1) {
//                     return true;
//                 }
      
//             }
//         }
//         return false;
//     }
// }



//FAST FOR ADD BUT SLOW FOR FIND
class TwoSum {
    Map<Integer, Integer> map;
    
    /** Initialize your data structure here. */
    public TwoSum() {
        map = new HashMap();
    }
    
    /** Add the number to an internal data structure.. */
    public void add(int number) {
        if (map.containsKey(number) == false) {
            map.put(number, 1);
        }
        else {
            map.put(number, 2);
        }
    }
    
    
    /** Find if there exists any pair of numbers which sum is equal to the value. */
    public boolean find(int value) {
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if (map.containsKey(value - entry.getKey())) {
                if (value != 2 * entry.getKey() || map.get(entry.getKey()) == 2) {
                    return true;
                }
            }
        }
        return false;
    }
}




//TLE =====> FAST FOR FIND BUT SLOW FOR ADD
// class TwoSum {
//     Set<Integer> sum;
//     Set<Integer> num;
//     /** Initialize your data structure here. */
//     public TwoSum() {
//         sum = new HashSet();
//         num = new HashSet();
//     }
    
//     /** Add the number to an internal data structure.. */
//     public void add(int number) {
//         // if (num.contains(number)) {
//         //     sum.add(2 * number);
//         // }
//         // else {
//         //     for (int element : num) {
//         //         sum.add(element + number);
//         //     }
//         //     num.add(number);
//         // }
        
//         if(num.contains(number)){
//             sum.add(number * 2);
//         }else{
//             Iterator<Integer> iter = num.iterator();
//             while(iter.hasNext()){
//                 sum.add(iter.next() + number);
//             }
//             num.add(number);
//         }
        
        
  
//     }
    
    
//     /** Find if there exists any pair of numbers which sum is equal to the value. */
//     public boolean find(int value) {
//         return sum.contains(value);
//     }
// }


/**
 * Your TwoSum object will be instantiated and called as such:
 * TwoSum obj = new TwoSum();
 * obj.add(number);
 * boolean param_2 = obj.find(value);
 */









// set to store all sum ====> TLE
// class TwoSum {
//     List<Integer> list;
//     Set<Integer> set;
    
//     /** Initialize your data structure here. */
//     public TwoSum() {
//         list = new ArrayList();
//         set = new HashSet();
//     }
    
//     /** Add the number to an internal data structure.. */
//     public void add(int number) {

//         if (list.size() == 0){
//             list.add(number);
//             return;
//         }
        
//         for (int i : list) {
//             set.add(i + number);
//         }
//         list.add(number);
//     }
    
//     /** Find if there exists any pair of numbers which sum is equal to the value. */
//     public boolean find(int value) {
//         return set.contains(value);
//     }
    
// }

// /**
//  * Your TwoSum object will be instantiated and called as such:
//  * TwoSum obj = new TwoSum();
//  * obj.add(number);
//  * boolean param_2 = obj.find(value);
//  */
```





## 454 [4Sum II](https://leetcode.com/problems/4sum-ii)    

```java
// class Solution {
//     public int fourSumCount(int[] A, int[] B, int[] C, int[] D) {
//         int res = 0;
//         for (int element : D) {
//             res += threeSumCount(A, B, C, -element);
//         }
//         return res;
//     }
    
//     private int threeSumCount(int[] A, int[] B, int[] C, int sum) {
//         int res = 0;
//         for (int element : C) {
//             res += twoSumCount(A, B, sum - element);
//         }
//         return res;
//     }
    
//     private int twoSumCount(int[] A, int[] B, int sum) {
//         Map<Integer, Integer> map = new HashMap();
//         for (int i = 0; i < A.length; i++) {
//             map.put(A[i], map.getOrDefault(A[i], 0) + 1);
//         }
        
//         int res = 0;
//         for (int i = 0; i < B.length; i++) {
//             int target = sum - B[i];
//             if (map.containsKey(target) == true) {
//                 res += map.get(target);
//             }
//         }
//         return res;
//     }
// }





class Solution {
    public int fourSumCount(int[] A, int[] B, int[] C, int[] D) {
        int res = 0;
        Map<Integer, Integer> map = new HashMap();
//         for (int a : A) {
//             for (int b : B) {
//                 map.put(a + b, map.getOrDefault(a + b, 0) + 1);
//             }
//         }
        
//         for (int c : C) {
//             for (int d : D) {
//                 res += map.getOrDefault(-c-d,0);
//             }
//         }
        
        for (int c : C) {
            for (int d : D) {
                map.put(c + d, map.getOrDefault(c + d, 0) + 1);
            }
        }
        
        for (int a : A) {
            for (int b : B) {
                res += map.getOrDefault(-a-b,0);
            }
        }
        return res;
    }
}
```





## 347 [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements)    

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap();
        for (int i : nums) {
            map.put(i, map.getOrDefault(i, 0) + 1);
        }
        List<Integer>[] fre = new ArrayList[nums.length];
        
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if (fre[entry.getValue() - 1] == null) {
                fre[entry.getValue() - 1] = new ArrayList();
            }
            fre[entry.getValue() - 1].add(entry.getKey());
        }
        
        List<Integer> list = new ArrayList();
        
        // int num = 0;
        // for (int i = fre.length - 1; i >= 0; i--) {
        //     //System.out.println(fre[i]);
        //     if (fre[i] != null) {
        //         for (int element : fre[i]) {
        //             list.add(element);
        //             num++;
        //             if (num == k) {
        //                 return list;
        //             }
        //         }
        //     }
        // }
        
        
        int num = 0;
        for (int i = fre.length - 1; i >= 0 && list.size() < k; i--) {
            if (fre[i] != null) {
                list.addAll(fre[i]);
            }
        }
        
        if (list.size() != k) {
            throw new IllegalArgumentException("wrong with k");
        }
        
        return list;
    }
}



// class Solution {
//     public List<Integer> topKFrequent(int[] nums, int k) {
//         Map<Integer, Integer> map = new HashMap();
//         //O(n)
//         for (int i : nums) {
//             map.put(i, map.getOrDefault(i, 0) + 1);
//         }
        
//         //O(log(1) + log(2) + log(3) + ... + log(n)) 
//         TreeMap<Integer, List<Integer>> fre = new TreeMap();
//         for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
//             //log(k)
//             if (fre.containsKey(entry.getValue()) == false) {
//                 //log(k)
//                 fre.put(entry.getValue(), new ArrayList());
//             }
//             fre.get(entry.getValue()).add(entry.getKey());
//         }
        
//         List<Integer> list = new ArrayList();
        
        
//         // for (Map.Entry<Integer, List<Integer>> entry : fre.entrySet()) {
//         //     System.out.println(entry.getKey());
//         //     System.out.println(entry.getValue());
//         // }
        
//         while (list.size() < k) {
//             //Map.Entry<Integer, List<Integer>> entry = fre.pollLastEntry();
//             list.addAll(fre.pollLastEntry().getValue());
//         }
        
//         if (list.size() != k) {
//             throw new IllegalArgumentException("wrong with k");
//         }
        
//         return list;
//     }
// }



// class Solution {
//     public List<Integer> topKFrequent(int[] nums, int k) {
//         Map<Integer, Integer> map = new HashMap();
//         //O(n)
//         for (int ele : nums) {
//             map.put(ele, map.getOrDefault(ele, 0) + 1);
//         }
        
//         Comparator<Map.Entry<Integer, Integer>> comptor = new cmptor();
//         PriorityQueue<Map.Entry<Integer, Integer>> heap = new PriorityQueue(comptor);
        
//         //O(nlogk)
//         for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
//             // offer before poll !!!!!!
//             // [1,1,1,2,2,3] => 2, 1 => 2, 1, 3 => 2, 1
//             // if offer after poll => 2, 1 => 1 => 1, 3
//             heap.offer(entry);
//             if (heap.size() > k) {
//                 heap.poll();
//             }
//         }
        
//         List<Integer> res = new ArrayList();
    
//         while (heap.isEmpty() == false) {
//             res.add(heap.poll().getKey());
//         }
    
//         //O(klogk)
//         Collections.reverse(res);
//         return res;
//     }
    
//     private class cmptor implements Comparator<Map.Entry<Integer, Integer>> {
//         //@override
//         public int compare(Map.Entry<Integer, Integer> a, Map.Entry<Integer, Integer> b) {
//             return a.getValue() - b.getValue();
//         }
//     }
// }


// class Solution {
//     public List<Integer> topKFrequent(int[] nums, int k) {
//         Map<Integer, Integer> map = new HashMap();
//         //O(n)
//         for (int ele : nums) {
//             map.put(ele, map.getOrDefault(ele, 0) + 1);
//         }
        
//         // minheap
//         PriorityQueue<Integer> heap = new PriorityQueue((n1, n2) -> map.get(n1) - map.get(n2));
        
//         //O(nlogk)
//         for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
//             heap.offer(entry.getKey());
//             if (heap.size() > k) {
//                 heap.poll();
//             }
//         }
        
//         List<Integer> res = new ArrayList();
    
//         while (heap.isEmpty() == false) {
//             res.add(heap.poll());
//         }
    
//         //O(k)
//         Collections.reverse(res);
//         return res;
//     }
// }


// class Solution {
//     public List<Integer> topKFrequent(int[] nums, int k) {
//         Map<Integer, Integer> map = new HashMap();
//         //O(n)
//         for (int ele : nums) {
//             map.put(ele, map.getOrDefault(ele, 0) + 1);
//         }
        
//         // maxheap
//         PriorityQueue<Integer> heap = new PriorityQueue((n1, n2) -> map.get(n2) - map.get(n1));
        
//         //O(nlogn)
//         for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
//             heap.offer(entry.getKey());
//         }
        
//         List<Integer> res = new ArrayList();
//         //O(klogn)
//         while (res.size() < k) {
//             res.add(heap.poll());
//         }
//         return res;
//     }
    
// }


// class Solution {
//   public List<Integer> topKFrequent(int[] nums, int k) {
//     // build hash map : character and how often it appears
//     HashMap<Integer, Integer> count = new HashMap();
//     for (int n: nums) {
//       count.put(n, count.getOrDefault(n, 0) + 1);
//     }

//     // init heap 'the less frequent element first'
//     PriorityQueue<Integer> heap =
//             new PriorityQueue<Integer>((n1, n2) -> count.get(n1) - count.get(n2));

//     // keep k top frequent elements in the heap
//     for (int n: count.keySet()) {
//       heap.add(n);
//       if (heap.size() > k)
//         heap.poll();
//     }

//     // build output list
//     List<Integer> top_k = new LinkedList();
//     while (!heap.isEmpty())
//       top_k.add(heap.poll());
//     Collections.reverse(top_k);
//     return top_k;
//   }
// }



```





## 288[Unique Word Abbreviation](https://leetcode.com/problems/unique-word-abbreviation)    

```java
// class ValidWordAbbr {
//     Map<String, Set<String>> map;
//     public ValidWordAbbr(String[] dictionary) {
//         map = new HashMap();
//         for (String str : dictionary) {
//             String abbr = getValidWordAbbr(str);
//             if (map.containsKey(abbr) == false) {
//                  map.put(abbr, new HashSet());
//             }
//             map.get(abbr).add(str);
//         }
//     }
    
//     public boolean isUnique(String word) {
//         String abbr = getValidWordAbbr(word);
//         if (map.containsKey(abbr) == false) {
//             return true;
//         }
//         Set<String> set = map.get(abbr);
//         //return set.size() == 1 && set.iterator().next().equals(word);
//         return set.size() == 1 && set.contains(word);
//     }
    
//     private String getValidWordAbbr(String str) {
//         if (str.length() <= 2) {
//             return str;
//         }
//         int len = str.length();
//         //String res = "" + str.charAt(0) + (len - 2) + str.charAt(len - 1);
//         String res = str.charAt(0) + Integer.toString(len - 2) + str.charAt(len - 1);
//         //String res = str.substring(0, 1) + (len - 2) + str.substring(len - 1, len);
//         return res;
//     }
// }

// /**
//  * Your ValidWordAbbr object will be instantiated and called as such:
//  * ValidWordAbbr obj = new ValidWordAbbr(dictionary);
//  * boolean param_1 = obj.isUnique(word);
//  */




// class ValidWordAbbr {
//     Map<String, Boolean> map;
//     Set<String> set;
    
//     public ValidWordAbbr(String[] dictionary) {
//         map = new HashMap();
//         set = new HashSet(Arrays.asList(dictionary));
        
//         for (String str : set) {
//             String abbr = getValidWordAbbr(str);
//             map.put(abbr, !map.containsKey(abbr));
//         }
//     }
    
//     public boolean isUnique(String word) {
//         String abbr = getValidWordAbbr(word);
//         return map.get(abbr) == null || (map.get(abbr) == true && set.contains(word));
//     }
    
//     private String getValidWordAbbr(String str) {
//         if (str.length() <= 2) {
//             return str;
//         }
//         int len = str.length();
//         //String res = "" + str.charAt(0) + (len - 2) + str.charAt(len - 1);
//         String res = str.charAt(0) + Integer.toString(len - 2) + str.charAt(len - 1);
//         //String res = str.substring(0, 1) + (len - 2) + str.substring(len - 1, len);
//         return res;
//     }
// }

// /**
//  * Your ValidWordAbbr object will be instantiated and called as such:
//  * ValidWordAbbr obj = new ValidWordAbbr(dictionary);
//  * boolean param_1 = obj.isUnique(word);
//  */


class ValidWordAbbr {
    Map<String, String> map;
    
    public ValidWordAbbr(String[] dictionary) {
        map = new HashMap();
        
        for (String str : dictionary) {
            String abbr = getValidWordAbbr(str);
            if (map.containsKey(abbr)){
                if (map.get(abbr).equals(str) == false) {
                    map.put(abbr, "");
                }
            }
            else {
                map.put(abbr, str);
            }
            
        }
    }
    
    public boolean isUnique(String word) {
        String abbr = getValidWordAbbr(word);
        return map.containsKey(abbr) == false || map.get(abbr).equals(word);
    }
    
    private String getValidWordAbbr(String str) {
        if (str.length() <= 2) {
            return str;
        }
        int len = str.length();
        //String res = "" + str.charAt(0) + (len - 2) + str.charAt(len - 1);
        String res = str.charAt(0) + Integer.toString(len - 2) + str.charAt(len - 1);
        //String res = str.substring(0, 1) + (len - 2) + str.substring(len - 1, len);
        return res;
    }
}

// /**
//  * Your ValidWordAbbr object will be instantiated and called as such:
//  * ValidWordAbbr obj = new ValidWordAbbr(dictionary);
//  * boolean param_1 = obj.isUnique(word);
//  */


// public class ValidWordAbbr {
//     HashMap<String, String> map;
//     public ValidWordAbbr(String[] dictionary) {
//         map = new HashMap<String, String>();
//         for(String str:dictionary){
//             String key = getKey(str);
//             // If there is more than one string belong to the same key
//             // then the key will be invalid, we set the value to ""
//             if(map.containsKey(key)){
//                 if(!map.get(key).equals(str)){
//                     map.put(key, "");
//                 }
//             }
//             else{
//                 map.put(key, str);
//             }
//         }
//     }

//     public boolean isUnique(String word) {
//         return !map.containsKey(getKey(word))||map.get(getKey(word)).equals(word);
//     }
    
//     String getKey(String str){
//         if(str.length()<=2) return str;
//         return str.charAt(0)+Integer.toString(str.length()-2)+str.charAt(str.length()-1);
//     }
// }
```



## 380 [Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1)    

```java
// class RandomizedSet {
//     int bucket = 10000;
//     List<Integer>[] arr;
//     List<Integer> existingBucketList;
//     /** Initialize your data structure here. */
//     public RandomizedSet() {
//         arr = (List<Integer>[])new ArrayList[bucket];
//         existingBucketList = new ArrayList();
//     }
    
//     /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
//     public boolean insert(int val) {
//         List<Integer> list = arr[hash(val)];
//         if (list == null) {
//             list = new ArrayList();
//         }
//         for (int element : list) {
//             if (element == val) {
//                 return false;
//             }
//         }
//         list.add(val);
//         arr[hash(val)] = list;
//         //System.out.println("add--" +  arr[hash(val)]);
//         existingBucketList.add(hash(val));
//         return true;
//     }
    
//     /** Removes a value from the set. Returns true if the set contained the specified element. */
//     public boolean remove(int val) {
//         List<Integer> list = arr[hash(val)];
       
//         // System.out.print("remove:---" + list);
//         // System.out.print(hash(val));
//         if (list == null) {
//             return false;
//         }
//         for (int i = 0; i < list.size(); i++) {
           
//             if (list.get(i) == val) {
                
//                 list.remove(i);
    
//                 for (int k = 0; k < existingBucketList.size(); k++) {
//                     if (existingBucketList.get(k).equals(hash(val))) {
//                         existingBucketList.remove(k);
//                     }
//                 }
                
                
//                 return true;
//             }
//         }
//         return false;
//     }
    
//     /** Get a random element from the set. */
//     public int getRandom() {
//         //System.out.println(existingBucketList);
//         //System.out.println((int)(Math.random() * (existingBucketList.size() - 1)));
        
//         int random = (int)(Math.random() * (existingBucketList.size()));
//         List<Integer> list = arr[hash(existingBucketList.get(random))];
//         //System.out.println(list);
//         //return -1;
//         return list.get((int)(Math.random() * list.size()));
//     }
    
//     private int hash(int num) {
//         return Math.abs(num) % bucket;
//     }
// }

// /**
//  * Your RandomizedSet object will be instantiated and called as such:
//  * RandomizedSet obj = new RandomizedSet();
//  * boolean param_1 = obj.insert(val);
//  * boolean param_2 = obj.remove(val);
//  * int param_3 = obj.getRandom();
//  */



class RandomizedSet {
    List<Integer> list;
    Map<Integer, Integer> map;
    /** Initialize your data structure here. */
    public RandomizedSet() {
        list = new ArrayList();
        map = new HashMap();
    }
    
    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    public boolean insert(int val) {
        if (map.containsKey(val)) {
            return false;
        }
        map.put(val, list.size());
        list.add(val);
        return true;
    }
    
    /** Removes a value from the set. Returns true if the set contained the specified element. */
    public boolean remove(int val) {
        if (map.containsKey(val) == false) {
            return false;
        }
        int index = map.get(val);
        int lastIndex = list.size() - 1;
        // put the lastone to the remove index and update map => remove index
        // This step is O(1) 
        // Do not do shifting!!!! which is O(n) !!!!!!
        if (index < lastIndex) {
            int lastOne = list.get(lastIndex);
            list.set(index, lastOne);
            map.put(lastOne, index);
        }
        // remove the lastindex, map remove val
        list.remove(lastIndex);
        map.remove(val);
        return true;
    }
    
    /** Get a random element from the set. */
    public int getRandom() {
        int random = (int)(Math.random() * (list.size()));
        return list.get(random);
    }

}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```





