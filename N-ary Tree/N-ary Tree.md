## 589  [N-ary Tree Preorder Traversal](https://leetcode.com/problems/n-ary-tree-preorder-traversal)  

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val,List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
// class Solution {
//     public List<Integer> preorder(Node root) {
//         if (root == null) {
//             return new ArrayList();
//         }
        
//         List<Integer> list = new ArrayList();
//         list.add(root.val);
//         for (Node child : root.children) {
//             list.addAll(preorder(child));
//         }
//         return list;
//     }
// }


// class Solution {
//     List<Integer> list = new ArrayList();
    
//     public List<Integer> preorder(Node root) {
//         if (root == null) {
//             return list;
//             //return new ArrayList();
//         }
        
//         list.add(root.val);
//         for (Node child : root.children) {
//             preorder(child);
//         }
//         return list;
//     }
// }


class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> list = new ArrayList();
        helper(list, root);
        return list;
    }
    
    private void helper (List<Integer> list, Node root) {
        if (root == null) {
            return;
        }
        
        list.add(root.val);
        for (Node child : root.children) {
            helper(list, child);
        }
    }
}
```





## 590 [N-ary Tree Postorder Traversal](https://leetcode.com/problems/n-ary-tree-postorder-traversal)  

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val,List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
// class Solution {
//     public List<Integer> postorder(Node root) {
//         if (root == null) {
//             return new ArrayList();
//         }
        
//         List<Integer> list = new ArrayList();
//         for (Node child : root.children) {
//             list.addAll(postorder(child));
//         }
//         list.add(root.val);
//         return list;
//     }
// }


// class Solution {
//     List<Integer> list = new ArrayList();
    
//     public List<Integer> postorder(Node root) {
//         if (root == null) {
//             return list;
//             //return new ArrayList();
//         }
        
       
//         for (Node child : root.children) {
//             postorder(child);
//         }
//         list.add(root.val);
//         return list;
//     }
// }


class Solution {
    public List<Integer> postorder(Node root) {
        List<Integer> list = new ArrayList();
        helper(list, root);
        return list;
    }
    
    private void helper (List<Integer> list, Node root) {
        if (root == null) {
            return;
        }
        
        for (Node child : root.children) {
            helper(list, child);
        }
        list.add(root.val);
    }
}
```





## 429 [N-ary Tree Level Order Traversal](https://leetcode.com/problems/n-ary-tree-level-order-traversal)    

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val,List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        if (root == null) {
            return new ArrayList();
        }
        
        Queue<Node> queue = new LinkedList();
        queue.offer(root);
        //queue.offer(null);

        List<List<Integer>> res = new ArrayList();
        
        while (queue.isEmpty() == false) {
            int size = queue.size();
            List<Integer> childList = new ArrayList();
            for (int i = 0; i < size; i++) {
                Node curr = queue.poll();
                childList.add(curr.val);
                for (Node child : curr.children) {
                    queue.offer(child);  
                }
            }
            res.add(childList);
        }
        return res;
    }
}
```





## 559 [Maximum Depth of N-ary Tree](https://leetcode.com/problems/maximum-depth-of-n-ary-tree)   

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val,List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
// class Solution {
//     public int maxDepth(Node root) {
//         if (root == null) {
//             return 0;
//         }
//         int[] height = new int[1];
//         preOrder(root, height, 1);
//         return height[0];
//     }
    
//     // //top-down: preorder
//     // private void preOrder(Node root, int[] height, int currH) {
//     //     if (root == null) {
//     //         return;
//     //     }
//     //     if (root.children.size() == 0) {
//     //         height[0] = Math.max(height[0], currH);
//     //     }
//     //     for (Node child : root.children) {
//     //         preOrder(child, height, currH + 1);
//     //     }
//     // }
    
//     // //top-down: preorder
//     // private void preOrder(Node root, int[] height, int currH) {
//     //     // if (root == null) {
//     //     //     return;
//     //     // }
//     //     if (root.children.size() == 0) {
//     //         height[0] = Math.max(height[0], currH);
//     //         return;
//     //     }
//     //     for (Node child : root.children) {
//     //         preOrder(child, height, currH + 1);
//     //     }
//     // }
// }




// class Solution {
//     //Bottom up: postOrder
//     public int maxDepth(Node root) {
//         if (root == null) {
//             return 0;
//         }
//         int res = 1;
//         //leaf root will not enter the for loop ==> res = 1
//         for (Node child : root.children) {
//             res = Math.max(res, maxDepth(child) + 1);
//         }
//         return res;
//     }
// }


// class Solution {
//     //BFS
//     public int maxDepth(Node root) {
//         if (root == null) {
//             return 0;
//         }
       
//         Queue<Node> queue = new LinkedList();
//         queue.offer(root);
//         int res = 0;
        
//         while (queue.isEmpty() == false) {
//             int size = queue.size();
//             res++;
//             for (int i = 0; i < size; i++) {
//                 Node curr = queue.poll();
//                 for (Node child : curr.children) {
//                     queue.offer(child);
//                 }
//             }
//         }
//         return res;
//     }
// }


class Solution {
    //BFS
    public int maxDepth(Node root) {
        if (root == null) {
            return 0;
        }
       
        Queue<Node> queue = new LinkedList();
        queue.offer(root);
        queue.offer(null);
        int res = 0;
        
        while (queue.isEmpty() == false) {
            Node curr = queue.poll();
            if (curr == null) {
                res++;
                if (queue.isEmpty() == false) {
                    queue.offer(null);
                }
            }
            else {
                for (Node child : curr.children) {
                    queue.offer(child);
                }
            }
        }
        return res;
    }
}
```





## 431 [Encode N-ary Tree to Binary Tree](https://leetcode.com/problems/encode-n-ary-tree-to-binary-tree)  

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val,List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Codec {

    // Encodes an n-ary tree to a binary tree.
    public TreeNode encode(Node root) {
        if (root == null) {
            return null;
        }
        TreeNode res = new TreeNode(root.val);
        TreeNode curr = res;
        // for (int i = 0; i < root.children.size(); i++) {
        //     if (i == 0) {
        //         curr.right = encode(root.children.get(0));
        //         curr = curr.right;
        //     }
        //     else {
        //         curr.left = encode(root.children.get(i));
        //         curr = curr.left;
        //     }
        // }
        
        
        if (root.children.size() > 0) {
            curr.right = encode(root.children.get(0));
            curr = curr.right;
        }
        
        for (int i = 1; i < root.children.size(); i++) {
            curr.left = encode(root.children.get(i));
            curr = curr.left;
        }
        return res;
    }

    // Decodes your binary tree to an n-ary tree.
    //preOrder => in, right, left
    public Node decode(TreeNode root) {

        if (root == null) {
            return null;
        }
        
        // Node res = new Node(root.val);
        // //children = new ArrayList, otherwise = null !!!!
        // res.children = new ArrayList();
        Node res = new Node(root.val, new ArrayList());

        // TreeNode curr = root;
        // if (curr.right != null) {
        //     //firstChild
        //     curr = curr.right;
        //     res.children.add(decode(curr));
        //     while (curr.left != null) {
        //         curr = curr.left;
        //         res.children.add(decode(curr));
        //     }
        // }
        
        TreeNode curr = root.right;
        while (curr != null) {
            res.children.add(decode(curr));
            curr = curr.left;
        }
        
        return res;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(root));
```





## 428 [Serialize and Deserialize N-ary Tree](https://leetcode.com/problems/serialize-and-deserialize-n-ary-tree)    

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val,List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Codec {

    // Encodes a tree to a single string.
    // preOrder
    public String serialize(Node root) {
        StringBuilder sb = new StringBuilder();
        buildSb(root, sb);
        //System.out.println(sb.toString());
        return sb.toString();
    }
    
    private void buildSb(Node parent, StringBuilder sb) {
        if (parent == null) {
            return;
        }
        sb.append(parent.val);
        sb.append(",");
        sb.append(parent.children.size());
        sb.append(",");
        for (Node child : parent.children) {
            buildSb(child, sb);
        }
    }
    
//     public String serialize(Node root) {
//         List<Integer> list = new ArrayList();
//         buildList(root, list);
      
//         StringBuilder sb = new StringBuilder();
//         for (int element : list) {
//             sb.append(element);
//             sb.append(',');
//         }
//         return sb.toString();
//     }
    
//     private void buildList(Node parent, List<Integer> list) {
//         if (parent == null) {
//             return;
//         }
//         list.add(parent.val);
//         list.add(parent.children.size());
//         for (Node child : parent.children) {
//             buildList(child, list);
//         }
//     }

    // Decodes your encoded data to tree.
    public Node deserialize(String data) {
        if (data.length() == 0) {
            return null;
        }
        String[] arr = data.split(",");
        Queue<String> queue = new LinkedList<String>(Arrays.asList(arr));
        return deserializeHelper(queue);
    }
    
    private Node deserializeHelper(Queue<String> queue) {
        Node parent = new Node(Integer.valueOf(queue.poll()), new ArrayList());
        int size = Integer.valueOf(queue.poll());
        while (size > 0) {
            parent.children.add(deserializeHelper(queue));
            size--;
        }
        return parent;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```



