## 98 Validate Binary Search Tree



```java
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
```



O(n) extra space

```java
public boolean isValidBST(TreeNode root) { 
    if (root == null) {
        return true;
    }
    ArrayList<Integer> inOrder = new ArrayList();
    inOrder(root, inOrder);
    // for (Integer element : inOrder) {
    //     System.out.println(element);
    // }

    if (inOrder.size() == 1) {
        return true;
    }

    for (int i = 1; i < inOrder.size(); i++) {

        if (inOrder.get(i) <= inOrder.get(i - 1)) {
            return false;
        }
    }
    return true;
}

private void inOrder(TreeNode root, ArrayList list) {
    if (root == null) {
        return;
    }
    inOrder(root.left, list);
    list.add(root.val);
    inOrder(root.right, list);
}
```









I will show you all how to tackle various tree questions using iterative inorder traversal. First one is the standard iterative inorder traversal using stack. Hope everyone agrees with this solution.



Question : [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)



```java
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    if(root == null) return list;
    Stack<TreeNode> stack = new Stack<>();
    while(root != null || !stack.empty()){
        while(root != null){
            stack.push(root);
            root = root.left;
        }
        root = stack.pop();
        list.add(root.val);
        root = root.right;
        
    }
    return list;
}
```



Now, we can use this structure to find the Kth smallest element in BST.



Question : [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)



```java
 public int kthSmallest(TreeNode root, int k) {
     Stack<TreeNode> stack = new Stack<>();
     while(root != null || !stack.isEmpty()) {
         while(root != null) {
             stack.push(root);    
             root = root.left;   
         } 
         root = stack.pop();
         if(--k == 0) break;
         root = root.right;
     }
     return root.val;
 }
```



We can also use this structure to solve BST validation question.



Question : [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)



```java
public boolean isValidBST(TreeNode root) {
   if (root == null) return true;
   Stack<TreeNode> stack = new Stack<>();
   TreeNode pre = null;
   while (root != null || !stack.isEmpty()) {
      while (root != null) {
         stack.push(root);
         root = root.left;
      }
      root = stack.pop();
      if(pre != null && root.val <= pre.val) return false;
      pre = root;
      root = root.right;
   }
   return true;
}
```







##285 Inorder Successor in BST



Successor

Stupid In-order way

```java
public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
    ArrayList<TreeNode> list = new ArrayList();
    int[] index = new int[1];
    helper(root, p, list, index);
    list.add(null);
    return list.get(index[0] + 1);
}

private void helper(TreeNode root, TreeNode p, ArrayList<TreeNode> list, int[] index) { 
    if (root == null) {
        return;
    }

    helper(root.left, p, list, index);
    list.add(root);
    if (root == p) {
        index[0] = list.size() - 1;
    }
    helper(root.right, p, list, index);
}
```



```java
public TreeNode successor(TreeNode root, TreeNode p) {
  if (root == null)
    return null;

  if (root.val <= p.val) {
    return successor(root.right, p);
  } else {
    TreeNode left = successor(root.left, p);
    return (left != null) ? left : root;
  }
}
```





The inorder traversal of a BST is the nodes in ascending order. To find a successor, you just need to find the smallest one that is larger than the given value since there are no duplicate values in a BST. It just like the binary search in a sorted list. The time complexity should be `O(h)` where h is the depth of the result node. `succ` is a pointer that keeps the possible successor. Whenever you go left the current root is the new possible successor, otherwise the it remains the same.



Only in a balanced BST `O(h) = O(log n)`. In the worst case `h` can be as large as `n`.



```java
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
```




Predecessor

```java
public TreeNode predecessor(TreeNode root, TreeNode p) {
  if (root == null)
    return null;

  if (root.val >= p.val) {
    return predecessor(root.left, p);
  } else {
    TreeNode right = predecessor(root.right, p);
    return (right != null) ? right : root;
  }
}
```





