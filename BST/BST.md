## 98[Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree)    

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
    
    public boolean isValidBST(TreeNode root) { 
        // if (root == null) {
        //     return true;
        // }
        return helper(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }
    
    private boolean helper (TreeNode root, long min, long max) {
        if (root == null) {
            return true;
        }
        if (root.val <= min || root.val >= max) {
            return false;
        }
        return helper(root.left, min, (long) root.val) && helper(root.right, (long) root.val, max);
    }

    
//     public boolean isValidBST(TreeNode root) { 
//         if (root == null) {
//             return true;
//         }
//         ArrayList<Integer> inOrder = new ArrayList();
//         inOrder(root, inOrder);
//         // for (Integer element : inOrder) {
//         //     System.out.println(element);
//         // }
     
//         if (inOrder.size() == 1) {
//             return true;
//         }
   
//         for (int i = 1; i < inOrder.size(); i++) {
           
//             if (inOrder.get(i) <= inOrder.get(i - 1)) {
//                 return false;
//             }
//         }
//         return true;
//     }
    
//     private void inOrder(TreeNode root, ArrayList list) {
//         if (root == null) {
//             return;
//         }
//         inOrder(root.left, list);
//         list.add(root.val);
//         inOrder(root.right, list);
//     }
}
```





## 285 [Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst)

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
//     public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
//         ArrayList<TreeNode> list = new ArrayList();
//         int[] index = new int[1];
//         helper(root, p, list, index);
//         list.add(null);
//         return list.get(index[0] + 1);
//     }
    
//     private void helper(TreeNode root, TreeNode p, ArrayList<TreeNode> list, int[] index) { 
//         if (root == null) {
//             return;
//         }
        
//         helper(root.left, p, list, index);
//         list.add(root);
//         if (root == p) {
//             index[0] = list.size() - 1;
//         }
//         helper(root.right, p, list, index);
//     }
    
//     public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
//         if (root == null) {
//             return null;
//         }
        
//         if (root.val <= p.val) {
//             return inorderSuccessor(root.right, p);
//         }
//         else {
//             TreeNode left = inorderSuccessor(root.left, p);
//             return left == null ? root : left;
//         }
//     }
    
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        TreeNode result = null;
        
        while (root != null) {
            if (root.val < p.val) {
                root = root.right;
            }
            else if (root.val > p.val){
                result = root;
                root = root.left;
            }
            else {
                root = root.right;
            }
        }
        
        return result;
    }
}
```





## 173 Binary Search Tree Iterator

```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

public class BSTIterator {
    Queue<Integer> queue = new LinkedList();
    
    public BSTIterator(TreeNode root) {
        inOrder(root, queue);
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !queue.isEmpty();
    
    }

    /** @return the next smallest number */
    public int next() {
        return queue.poll();
    }
    
    private void inOrder(TreeNode root, Queue<Integer> queue) {
        if (root == null) {
            return;
        }
        inOrder(root.left, queue);
        queue.offer(root.val);
        inOrder(root.right, queue);
    }
}

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = new BSTIterator(root);
 * while (i.hasNext()) v[f()] = i.next();
 */
```



## 700 [Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree)

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
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null) {
            return null;
        }
        TreeNode cur = root;
        while (cur != null) {
            if (cur.val < val) {
                cur = cur.right;
            }
            else if (cur.val > val) {
                cur = cur.left;
            }
            else {
                return cur;
            }
        }
        return null;
    }
    
    // public TreeNode searchBST(TreeNode root, int val) {
    //     if (root == null) {
    //         return null;
    //     }
    //     TreeNode cur = root;
    //     if (cur.val < val) {
    //         return searchBST(cur.right, val);
    //     }
    //     else if (cur.val > val) {
    //         return searchBST(cur.left, val);
    //     }
    //     else {
    //         return cur;
    //     }
    // }
}
```





## 701 [Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree)  

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
    //iterative
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        TreeNode parent = null;
        TreeNode curr = root;
        while (curr != null) {
            parent = curr;
            if (curr.val <= val) {
                curr = curr.right;
            }
            else if (curr.val > val) {
                curr = curr.left;
            }
            // else {
            //     return root;
            // }
        }
        if (parent.val < val) {
            parent.right = new TreeNode(val);
        } 
        else if (parent.val > val) {
            parent.left = new TreeNode(val);
        }
        return root;
    }
    
    
    //recursion
    // public TreeNode insertIntoBST(TreeNode root, int val) {
    //     if (root == null) {
    //         return new TreeNode(val);
    //     }
    //     if (root.val < val) {
    //         root.right = insertIntoBST(root.right, val);
    //     } 
    //     else if (root.val > val) {
    //         root.left = insertIntoBST(root.left, val);
    //     }
    //     else {
    //         root.right = insertIntoBST(root.right, val);
    //     }
    //     return root;
    // }
}
```







## 450 [Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst)   

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
    
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) {
            return null;
        }
        
        if (root.val < key) {
            root.right = deleteNode(root.right, key);
        }
        else if (root.val > key) {
            root.left = deleteNode(root.left, key);
        }
        else {
          
            if (root.left == null) {
                return root.right;
            }
            if (root.right == null) {
                return root.left;
            }
            TreeNode precesor =  findPrecesor(root);
            root.val = precesor.val;
            root.left = deleteNode(root.left, precesor.val);
        }
        return root;
    }
    
    //find the succesor of the root of BST
    private TreeNode findPrecesor(TreeNode root) {
        if (root == null || root.left == null) {
            return null;
        }
        TreeNode curr = root.left;
        while (curr.right != null) {
            curr = curr.right;
        }
        return curr;
    }
    
    
//     public TreeNode deleteNode(TreeNode root, int key) {
//         if (root == null) {
//             return null;
//         }
        
//         if (root.val < key) {
//             root.right = deleteNode(root.right, key);
//         }
//         else if (root.val > key) {
//             root.left = deleteNode(root.left, key);
//         }
//         else {
          
//             if (root.left == null) {
//                 return root.right;
//             }
//             if (root.right == null) {
//                 return root.left;
//             }
//             TreeNode succesor =  findSuccesor(root);
//             root.val = succesor.val;
//             root.right = deleteNode(root.right, succesor.val);
//         }
//         return root;
//     }
    
//     //find the succesor of the root of BST
//     private TreeNode findSuccesor(TreeNode root) {
//         if (root == null || root.right == null) {
//             return null;
//         }
//         TreeNode curr = root.right;
//         while (curr.left != null) {
//             curr = curr.left;
//         }
//         return curr;
//     }
}
```





## 703 [Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream)  

```java
class KthLargest {
    
    class TreeNode {
        int val;
        int count;
        TreeNode left;
        TreeNode right;
        TreeNode (int val) {
            this.val = val;
            this.count = 1;
        }
    }
    
    TreeNode root;
    int k;
    
    public KthLargest(int k, int[] nums) {
        for (int element : nums) {
            root = addTreeNode(root, element);
        }
        this.k = k;
    }
    
    public int add(int val) {
        root = addTreeNode(root, val);
        //return getKLargestValue(root, k);
        return getKLargestValue();
    }
    
    //recursion
    private TreeNode addTreeNode(TreeNode head, int val) {
        if (head == null) {
            return new TreeNode(val);
        }
        head.count++;
        
        if (val < head.val) {
            head.left = addTreeNode(head.left, val);
        }
        else {
            head.right = addTreeNode(head.right, val);
        }
        return head;
    }
    
    
    // iteration
//     private TreeNode addTreeNode(TreeNode head, int val) {
//         if (head == null) {
//             return new TreeNode(val);
//         }

//         TreeNode walker = head;
//         while (walker.left != null || walker.right != null) {
//             walker.count++;
//             if (val < walker.val) {
//                 if (walker.left == null) {
//                     break;
//                 }
//                 walker = walker.left;
//             }
//             else {
//                 if (walker.right == null) {
//                     break;
//                 }
//                 walker = walker.right;
//             }
//         }
        
//         walker.count++;
//         if (val < walker.val) {
//             walker.left = new TreeNode(val);
//         }
//         else {
//             walker.right = new TreeNode(val);
//         }
        
//         // System.out.println("head" + head.val);
//         // System.out.println("COUNT" + head.count);
//         return head;
//     }
    
    
    
    
    //recursion
    // private int getKLargestValue(TreeNode head, int count) {
    //     int pos = 1 + (head.right == null ? 0 : head.right.count);
    //     if (pos == count) {
    //         return head.val;
    //     }
    //     else if (count > pos) {
    //         count -= pos;
    //         return getKLargestValue(head.left, count);
    //     }
    //     else {
    //         return getKLargestValue(head.right, count);
    //     }
    // }
    
    
    
    
    
    //iteration
    private int getKLargestValue() {
        TreeNode walker = root;
        int count = k;
        // while (walker != null) {
        //    int pos = 1 + (walker.right == null ? 0 : walker.right.count);
        //    if (pos == count) {
        //         return walker.val;
        //    }
        //    else if (count > pos) {
        //         count -= pos;
        //         walker = walker.left;
        //    }
        //    else {
        //         walker = walker.right;
        //    }
        // }
        // return -1;
        
        
        //while (count != 0) {
        while (true) {
           int pos = 1 + (walker.right == null ? 0 : walker.right.count);
           if (pos == count) {
                break;
           }
           else if (count > pos) {
                count -= pos;
                walker = walker.left;
           }
           else {
                walker = walker.right;
           }
        }
        return walker.val;
    }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
```





## 235 [Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree)   

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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return null;
        }
        if (root == p) {
            return p;
        }
        if (root == q) {
            return q;
        }
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if (left == null) {
            return right;
        }
        if (right == null) {
            return left;
        }
        return root;
    }
}
```





## 220 [Contains Duplicate III](https://leetcode.com/problems/contains-duplicate-iii) 

```java
class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        if (nums == null || nums.length < 1 || k < 1 || t < 0) {
            return false;
        }
        
        // If Set<Integer>, the interface has no floor and ceiling function!!!
        //Set<Integer> set = new TreeSet();
        TreeSet<Long> set = new TreeSet();
        for (int i = 0; i < nums.length; i++) {
            Long floor = set.floor((long)nums[i] + (long)t);
            Long ceil = set.ceiling((long)nums[i] - (long)t);
            // System.out.println("floor" + ((long)nums[i] + (long)t));
            // System.out.println("floor" + floor);
            // System.out.println("ceil" + ((long)nums[i] - (long)t));
            // System.out.println("ceil" +ceil);
            
            
            //wrong!!!
            // Long floor = set.floor((long)(nums[i] + t)); //-2147483648 + 3 = -2147483645  -2147483647 + 3 = -2147483644
            // Long ceil = set.ceiling((long)(nums[i] - t)); //-2147483647 - 3 = 2147483645  -2147483647 - 3 = 2147483646 !!!!! wrong!!!!!
            // System.out.println("floor" + (long)(nums[i] + t));
            // System.out.println("floor" + floor);
            // System.out.println("ceil" + (long)(nums[i] - t));
            // System.out.println("ceil" +ceil);
            
            if ((floor != null && floor >= (long)nums[i]) || (ceil != null && ceil <= (long)nums[i])) {
                return true;
            }
            if (i >= k) {
                set.remove((long)nums[i - k]);
            }
            set.add((long)nums[i]);
        }
        return false;
    }
}
```





## 110 [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree)  

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
//      T(n) = 2 * T(n / 2) + O(n)  O(n * log(n)) 
//     public boolean isBalanced(TreeNode root) {
//         if (root == null) {
//             return true;
//         }
//         int leftHeight = 0;
//         int rightHeight = 0;
//         if (Math.abs(depth(root.left) - depth(root.right)) > 1) {
//             return false;
//         }
//         return isBalanced(root.left) && isBalanced(root.right);
//     }
    
//     private int depth(TreeNode root) {
//         if (root == null) {
//             return 0;
//         }
//         int result = 0;
//         result = Math.max(depth(root.left),depth(root.right)) + 1;
//         return result;
//     }
    
    
//     private Map<TreeNode, Integer> map = new HashMap();
//     public boolean isBalanced(TreeNode root) {
//         if (root == null) {
//             return true;
//         }
        
//         if (map.size() == 0) {
//             depth(root);
//         }
//         if (Math.abs(map.get(root.left) - map.get(root.right)) > 1) {
//             return false;
//         }
//         return isBalanced(root.left) && isBalanced(root.right);
//     }
    
//     private int depth(TreeNode root) {
//         if (root == null) {
//             map.put(root, 0);
//             return 0;
//         }
//         int result = 0;
//         result = Math.max(depth(root.left),depth(root.right)) + 1;
//         map.put(root, result);
//         return result;
//     }
    
    
//     private Map<TreeNode, Integer> map = new HashMap();
//     public boolean isBalanced(TreeNode root) {
//         // if (root == null) {
//         //     return true;
//         // }
        
//         // depth(root);
//         // return map.get(root) != -1;
        
//         //hashmap is not necessary any more
//         return depth(root) != -1;
//     }
    
//     private int depth(TreeNode root) {
//         if (root == null) {
//             map.put(root, 0);
//             return 0;
//         }
//         int left = depth(root.left);
//         int right = depth(root.right);
//         if (left == -1) {
//             map.put(root, -1);
//             return -1;
//         }
//         if (right == -1 ) {
//             map.put(root, -1);
//             return -1; 
//         }
//         if (Math.abs(left - right) > 1) {
//             map.put(root, -1);
//             return -1;
//         }
//         int result = Math.max(left,right) + 1;
//         map.put(root, result);
//         return result;
//     }
    
    
    
    
    public boolean isBalanced(TreeNode root) {
        return depth(root) != -1;
    }
    
    private int depth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = depth(root.left);
        if (left == -1) {
            return -1;
        }
        int right = depth(root.right);
        if (right == -1) {
            return -1;
        }
        if (Math.abs(left - right) > 1) {
            return -1;
        }
        return Math.max(left, right) + 1;
    }
}
```





## 108 [Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree)    

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
    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums == null || nums.length == 0) {
            return null;
        }
        return helper(nums, 0, nums.length -1);
    }
    
    private TreeNode helper(int[] nums, int left, int right) {
        if (left > right) {
            return null;
        }
        
        int mid = left + (right - left) / 2;
        TreeNode res = new TreeNode(nums[mid]);
        res.left = helper(nums, left, mid - 1);
        res.right = helper(nums, mid + 1, right);
        return res;
    }
}
```





