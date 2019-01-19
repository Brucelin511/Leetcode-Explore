## 144 [Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal)    

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
    // public List<Integer> preorderTraversal(TreeNode root) {
    //     if (root == null) {
    //         return new ArrayList<Integer>();
    //     }
    //     List<Integer> mid = new ArrayList();
    //     mid.add(root.val);
    //     List<Integer> pre = preorderTraversal(root.left);
    //     mid.addAll(pre);
    //     List<Integer> after = preorderTraversal(root.right);
    //     mid.addAll(after);
    //     return mid;
    // }
    
//     version 2
//     public List<Integer> preorderTraversal(TreeNode root) {
//         List<Integer> result = new ArrayList();
//         preorderTraversalHelper(root, result);
//         return result;
//     }
    
//     private void preorderTraversalHelper(TreeNode root, List<Integer> result) {
//         if (root == null) {
//             return;
//         }
//         result.add(root.val);
//         preorderTraversalHelper(root.left, result);
//         preorderTraversalHelper(root.right, result);
//     }
    
    //version 3
    // public List<Integer> preorderTraversal(TreeNode root) {
    //     List<Integer> result = new ArrayList();
    //     Stack<TreeNode> stack = new Stack();
    //     if (root == null) {
    //         return result;
    //     }
    //     stack.push(root);
    //     while (!stack.isEmpty()) {
    //         TreeNode currNode = stack.pop();
    //         result.add(currNode.val);
    //         if (currNode.right != null) {
    //             stack.push(currNode.right);
    //         }
    //         if (currNode.left != null) {
    //             stack.push(currNode.left);
    //         }            
    //     }
    //     return result;
    // }
    
    //version 4
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList();
        Stack<TreeNode> stack = new Stack();
        if (root == null) {
            return result;
        }
        TreeNode currNode = root;
        while (currNode != null || !stack.isEmpty()) {
            if (currNode != null) {
                stack.push(currNode);
                result.add(currNode.val);
                currNode = currNode.left;
            } else {
                currNode = stack.pop();
                currNode = currNode.right;
            }  
        }
        return result;
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





## 145 [Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal)  

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
    //version1
//     public List<Integer> postorderTraversal(TreeNode root) {
//         if (root == null) {
//                 return new ArrayList<Integer>();
//             }     
        
//             List<Integer> pre = postorderTraversal(root.left);
//             List<Integer> after = postorderTraversal(root.right);
//             pre.addAll(after);
//             pre.add(root.val);
//             return pre;
//     }
    
    //version 2
//     public List<Integer> postorderTraversal(TreeNode root) {
//         List<Integer> result = new ArrayList();
//         postorderTraversalHelper(root, result);
//         return result;
//     }
    
//     private void postorderTraversalHelper(TreeNode root, List<Integer> result) {
//         if (root == null) {
//             return;
//         }
//         postorderTraversalHelper(root.left, result);
//         postorderTraversalHelper(root.right, result);
//         result.add(root.val);
//     }
    
    //version 3 iterative
    public List<Integer> postorderTraversal(TreeNode root) {
        // List<Integer> result = new LinkedList(); List has no method of addFirst
        LinkedList<Integer> result = new LinkedList();
        Stack<TreeNode> stack = new Stack();
        TreeNode cur = root;
        while (cur != null || !stack.isEmpty()) {
            if (cur != null) {
                stack.push(cur);
                result.addFirst(cur.val);
                cur = cur.right;
            } else {
                cur = stack.pop();
                cur = cur.left;
            }
        }
        return result;
    }
    
}
```





## 102 [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal)   

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList();
        List<List<Integer>> result = new LinkedList();
        if (root == null) {
            return result;
        }
        queue.offer(root);
        while (!queue.isEmpty()) {
            List<Integer> inner = new LinkedList();
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode currNode = queue.poll();
                inner.add(currNode.val);
                if (currNode.left != null) queue.offer(currNode.left);
                if (currNode.right != null) queue.offer(currNode.right);
            }
            result.add(inner);
        }
        return result;
    }
}
```





## 104 [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree)     

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
    //version 1 bottom-up
    //T(n) = 2 * T(n / 2) + O(1)  O(n) 
    // public int maxDepth(TreeNode root) {
    //     if (root == null) {
    //         return 0;
    //     }
    //     int left = maxDepth(root.left);
    //     int right = maxDepth(root.right);
    //     return Math.max(left, right) + 1;
    // }
    
    //version 2 top-down
    private int result = 0; 
    public int maxDepth(TreeNode root) {
        maxDepthHelper(root, 1);
        return result;
    }
    
    private void maxDepthHelper(TreeNode root, int depth) {
        if (root == null) {
            return;
        }
        if (root.left == null && root.right == null) {
            result = Math.max(result, depth);
            return;
        }
        maxDepthHelper(root.left, depth + 1);
        maxDepthHelper(root.right, depth + 1);
    }
}
```



## 101 [Symmetric Tree](https://leetcode.com/problems/symmetric-tree)   

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
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        return isSymmetricHelper(root.left, root.right);
    }
    
    private boolean isSymmetricHelper(TreeNode leftRoot, TreeNode rightRoot) {
        if (leftRoot == null && rightRoot == null) {
            return true;
        }
        if (leftRoot == null || rightRoot == null) {
            return false;
        }
        if (leftRoot.val != rightRoot.val) {
            return false;
        }
        boolean isLeft = isSymmetricHelper(leftRoot.left, rightRoot.right);
        boolean isRight = isSymmetricHelper(leftRoot.right, rightRoot.left);
        return isLeft && isRight;
    }
}
```





## 112 [Path Sum](https://leetcode.com/problems/path-sum)    

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
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        if (root.left == null && root.right == null) {
            return sum - root.val == 0;
        }
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
}
```





## 250 [Count Univalue Subtrees](https://leetcode.com/problems/count-univalue-subtrees)    

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
//     //version 1
//     private int num = 0;
//     public int countUnivalSubtrees(TreeNode root) {
//         isUnivalSubtrees(root);
//         return num;
//     }
    
//     private boolean isUnivalSubtrees(TreeNode root) {
//         if (root == null) {
//             return true;
//         }
        
//         boolean left = isUnivalSubtrees(root.left);
//         if (root.left != null && left) {
//             left = root.val == root.left.val;
//         } 
//         boolean right = isUnivalSubtrees(root.right);
//         if (root.right != null && right) {
//             right = root.val == root.right.val;
//         } 
//         boolean isUnivalSubtrees = left && right;
//         if (isUnivalSubtrees) {
//             num++;
//         }
//         return isUnivalSubtrees;
//     }
    
    
//     //version 1.2
//     private int num = 0;
//     public int countUnivalSubtrees(TreeNode root) {
//         isUnivalSubtrees(root);
//         return num;
//     }
    
//     private boolean isUnivalSubtrees(TreeNode root) {
//         if (root == null) {
//             return true;
//         }
//         boolean left = isUnivalSubtrees(root.left);
//         boolean right = isUnivalSubtrees(root.right);
//         if (left && right) {
//             if (root.left != null) {
//                 left = root.val == root.left.val;
//             } 
//             if (root.right != null) {
//                 right = root.val == root.right.val;
//             } 
//         }
//         boolean isUnivalSubtrees = left && right;
//         if (isUnivalSubtrees) {
//             num++;
//         }
//         return isUnivalSubtrees;
//     }
    
    //version 2
    // public int countUnivalSubtrees(TreeNode root) {
    //     int[] num = {0};
    //     isUnivalSubtrees(root, num);
    //     return num[0];
    // }
    
//     private boolean isUnivalSubtrees(TreeNode root, int[] num) {
//         if (root == null) {
//             return true;
//         }
        
//         boolean left = isUnivalSubtrees(root.left, num);
//         if (root.left != null && left) {
//             left = root.val == root.left.val;
//         } 
//         boolean right = isUnivalSubtrees(root.right, num);
//         if (root.right != null && right) {
//             right = root.val == root.right.val;
//         } 
//         boolean isUnivalSubtrees = left && right;
//         if (isUnivalSubtrees) {
//             num[0]++;
//         }
//         return isUnivalSubtrees;
//     }
    
//         //version 2.2
//     public int countUnivalSubtrees(TreeNode root) {
//         int[] num = {0};
//         isUnivalSubtrees(root, num);
//         return num[0];
//     }
    
//     private boolean isUnivalSubtrees(TreeNode root, int[] num) {
//         if (root == null) {
//             return true;
//         }
        
//         boolean left = isUnivalSubtrees(root.left, num);
//         boolean right = isUnivalSubtrees(root.right, num);
//         if (left && right) {
//             if (root.left != null) {
//                 left = root.val == root.left.val;
//             } 

//             if (root.right != null) {
//                 right = root.val == root.right.val;
//             } 
//         }
//         boolean isUnivalSubtrees = left && right;
//         if (isUnivalSubtrees) {
//             num[0]++;
//         }
//         return isUnivalSubtrees;
//     }
    
            //version 2.3
    public int countUnivalSubtrees(TreeNode root) {
        int[] num = {0};
        isUnivalSubtrees(root, num);
        return num[0];
    }
    
    private boolean isUnivalSubtrees(TreeNode root, int[] num) {
        if (root == null) {
            return true;
        }
        
        boolean left = isUnivalSubtrees(root.left, num);
        boolean right = isUnivalSubtrees(root.right, num);
        if (left && right) {
            if (root.left != null && root.val != root.left.val) {
                return false;
            } 

            if (root.right != null && root.val != root.right.val) {
                return false;
            } 
            num[0]++;
            return true;
        }
        return false;
    }
        
}

```





## 106 [Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal)   

```java
// /**
//  * Definition for a binary tree node.
//  * public class TreeNode {
//  *     int val;
//  *     TreeNode left;
//  *     TreeNode right;
//  *     TreeNode(int x) { val = x; }
//  * }
//  */
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if (inorder == null || postorder == null || inorder.length != postorder.length) {
            return null;
        }
        
        Map<Integer, Integer> map = new HashMap();
        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }
        return helper(inorder, 0, inorder.length - 1, postorder, 0, postorder.length - 1, map);  
    }
    
    private TreeNode helper (int[] inorder, int il, int ir, int[] postorder, int pl, int pr, Map<Integer, Integer> map) {
        if (il > ir || pl > pr) {
            return null;
        }
        int ri = map.get(postorder[pr]);
        TreeNode result = new TreeNode(inorder[ri]);
        
        result.left = helper(inorder, il, ri - 1, postorder, pl, pl + ri - 1 - il, map);
        result.right = helper(inorder, ri + 1, ir, postorder, pr + ri -ir , pr - 1, map);
        return result;
    }
}

```





## 105 [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal)  

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
//     public TreeNode buildTree(int[] preorder, int[] inorder) {
//         if (preorder == null || inorder == null || preorder.length != inorder.length) {
//             return null;
//         }
        
//         Map<Integer, Integer> map = new HashMap();
//         for (int i = 0; i < inorder.length; i++) {
//             map.put(inorder[i], i);
//         }
//         return helper(preorder, 0, preorder.length - 1, inorder, 0, inorder.length - 1, map);
//     }
    
//     private TreeNode helper(int[] preorder, int preL, int preR, int[] inorder, int inL, int inR, Map<Integer, Integer> map) {
//         if (preL > preR || inL > inR) {
//             return null;
//         }
        
//         int rI = map.get(preorder[preL]);
//         TreeNode root = new TreeNode(inorder[rI]);
//         root.left = helper(preorder, preL + 1, preL + rI - inL, inorder, inL, rI - 1, map);
//         root.right = helper(preorder, preR + rI + 1 - inR, preR, inorder, rI + 1, inR, map);
//         return root;
//     }
    
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        
        if (preorder == null || inorder == null || preorder.length != inorder.length) {
            return null;
        }
        
        Map<Integer, Integer> map = new HashMap();
        
        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i], i);
        }
        
        // return helper(preorder, 0, inorder, 0, inorder.length - 1, map);
        return helper(preorder, 0, preorder.length - 1, inorder, 0, inorder.length - 1, map);
    }
    
//     private TreeNode helper(int[] preorder, int preL, int[] inorder, int inL, int inR, Map<Integer, Integer> map) {
//         if (inL > inR) {
//             return null;
//         }
//         int rI = map.get(preorder[preL]);  
//         // TreeNode root = new TreeNode(inorder[rI]);
        
//         TreeNode root = new TreeNode(preorder[preL]);
//         root.left = helper(preorder, preL + 1, inorder, inL, rI - 1, map);
//         root.right = helper(preorder, preL + rI - inL + 1, inorder, rI + 1, inR, map);
//         // root.right = helper(preorder, preR + rI + 1 - inR, inorder, rI + 1, inR, map);
//         return root;
//     }
    
    private TreeNode helper(int[] preorder, int preL, int preR, int[] inorder, int inL, int inR, Map<Integer, Integer> map) {
        if (preL > preR || inL > inR) {
            return null;
        }
        int rI = map.get(preorder[preL]);  
        // TreeNode root = new TreeNode(inorder[rI]);
        TreeNode root = new TreeNode(preorder[preL]);
        
        root.left = helper(preorder, preL + 1, preL + rI - inL, inorder, inL, rI - 1, map);
        root.right = helper(preorder, preR + rI + 1 - inR, preR, inorder, rI + 1, inR, map);
        return root;
    }
}
```





## 116 [Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node)   

```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
//     public void connect(TreeLinkNode root) {
        
//         TreeLinkNode level = root;
//         while (level != null) {
//             TreeLinkNode curr = level;
//             while (curr != null) {
//                 if (curr.left != null && curr.right != null) {
//                   curr.left.next = curr.right;  
//                 }
//                 if (curr.right != null && curr.next != null) {
//                   curr.right.next = curr.next.left; 
//                 }
                
//                 curr = curr.next;
//             }
//             level = level.left;
//         }
//     }
    
    public void connect(TreeLinkNode root) {
        if (root == null) {
            return;
        }
        
        TreeLinkNode parent = root;  
        
        while (parent.left != null) {
            
            TreeLinkNode curr = parent;
            while (curr != null) {
                curr.left.next = curr.right;
                if (curr.next != null) {
                   curr.right.next = curr.next.left; 
                }
                curr = curr.next;
            }
            parent = parent.left;
        }
        
    }
}
```





## 117  [Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii)    

```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        TreeLinkNode curr = root;
        TreeLinkNode head = null;
        TreeLinkNode prev = null;
        
        while (curr != null) {
            while (curr != null) {
                
                if (curr.left != null) {
                    if (prev != null) {
                        prev.next = curr.left;
                    } else {
                        head = curr.left;
                    }
                    prev = curr.left;
                }
                
                if (curr.right != null) {
                    if (prev != null) {
                        prev.next = curr.right;
                    } else {
                        head = curr.right;
                    }
                    prev = curr.right;
                }
                
                curr = curr.next;
            }
            
            curr = head;
            head = null;
            prev = null;
        }
    }
}
```





## 236 [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree)    

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
        if (root == null || root == p || root == q) {
            return root;
        }
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        return left == null ? right : right == null ? left : root;
    }
}
```



## 297 [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree)    

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
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        // if (root == null) {
        //     return "#";
        // }
        
        StringBuilder sb = new StringBuilder();
        Queue<TreeNode> queue = new LinkedList();
        queue.offer(root);
        while (!queue.isEmpty()) {
            TreeNode head = queue.poll();
            if (head == null) {
                sb.append("#").append(",");
                continue;
            } 
            sb.append(head.val).append(",");
            queue.offer(head.left);
            queue.offer(head.right);
        }
        //System.out.print(sb.toString());
        return sb.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        // if (data.equals("#")) {
        //     return null;
        // }
        
        Queue<TreeNode> queue = new LinkedList();
        String[] array = data.split(",");
        
        if (array[0].equals("#")) {
            return null;
        }
        
        TreeNode root = new TreeNode(Integer.valueOf(array[0]));
        queue.offer(root);
        
        for (int i = 1; i < array.length; i++) {
            TreeNode head = queue.poll();
            if (!array[i].equals("#")) {
                TreeNode left = new TreeNode(Integer.valueOf(array[i]));
                queue.offer(left);
                head.left = left;
            }
            
            if (!array[++i].equals("#")) {
                TreeNode right = new TreeNode(Integer.valueOf(array[i]));
                queue.offer(right);
                head.right = right;
            }
        }
        
        return root;
    }
}


//dfs
// public class Codec {
//     // Codec codec = new Codec();
//     // codec.deserialize(codec.serialize(root));
//     // Encodes a tree to a single string.
//     public String serialize(TreeNode root) {
//         StringBuilder sb = new StringBuilder();
//         buildString(root, sb);
//         return sb.toString();
//     }
    
//     private void buildString(TreeNode root, StringBuilder sb) {
//         if (root == null) {
//             sb.append("#").append(",");
//         }
//         else {
//             sb.append(root.val).append(",");
//             buildString(root.left, sb);
//             buildString(root.right, sb);
//         }
//     }

//     // Decodes your encoded data to tree.
//     public TreeNode deserialize(String data) {
//         String[] array = data.split(",");
//         Queue<String> queue = new LinkedList();
//         queue.addAll(Arrays.asList(array));
//         return buildTreeNode(queue);
//     }
    
//     private TreeNode buildTreeNode(Queue<String> queue) {
//         String val = queue.poll();
//         if (val.equals("#")) {
//             return null;
//         } else {
//             TreeNode head = new TreeNode(Integer.valueOf(val));
//             head.left = buildTreeNode(queue);
//             head.right = buildTreeNode(queue);
//             return head;
//         }
//     }
// }

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```







