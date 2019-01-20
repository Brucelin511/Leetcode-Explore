## 707 [Design Linked List](https://leetcode.com/problems/design-linked-list)    

```java
class MyLinkedList {
    private Node head;
    
    private class Node {
        int val;
        Node next;
        Node prev;
        
        Node(int val) {
            this.val = val;
            // this.next = null;
            // this.prev = null;
        }
        Node() {
            // this.next = null;
        }
    }

    
    /** Initialize your data structure here. */
    public MyLinkedList() {
        Node head = new Node();
        // Node head = null;
    }
    
    /** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
    public int get(int index) {
        int i = 0;
        Node curr = head;
        while (i < index && curr != null) {
            curr = curr.next;
            i++;
        }
        if (curr == null) {
            //print();
            return -1;
        }
        //print();
        return curr.val;
        
    }
    
    /** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
    public void addAtHead(int val) {
        Node newHead = new Node(val);
        
        if (this.head != null) {
            this.head.prev = newHead;
        }
        newHead.next = this.head;
        
        this.head = newHead;
        //print();
    }
    
    /** Append a node of value val to the last element of the linked list. */
    public void addAtTail(int val) {
        if (this.head == null) {
            this.head = new Node(val);
            //print();
            return;
        }
        Node curr = this.head;
        while (curr.next != null) {
            curr = curr.next;
        }
        Node last = new Node(val);
        last.prev = curr;
        curr.next = last;
        //print();
    }
    
    /** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
    public void addAtIndex(int index, int val) {
        if (index == 0) {
            
            Node newHead = new Node(val);
            if (this.head != null) {
                this.head.prev = newHead;
            }
            newHead.next = this.head;
            
            this.head = newHead;
            
            //print();
            return;
        }
        
        int i = 0;
        Node prev = this.head;
        while (i < index - 1 && prev != null) {
            prev = prev.next;
            i++;
        }

        if (prev == null) {
            //print();
            return;
        }
        Node insertNode = new Node(val);
        
        insertNode.next = prev.next;
        insertNode.prev = prev;
        
        if (prev.next != null) {
            prev.next.prev = insertNode;  
        }
        prev.next = insertNode;
 
        //print();
    }
    
    /** Delete the index-th node in the linked list, if the index is valid. */
    public void deleteAtIndex(int index) {
        if (this.head == null) {
            //print();
            return;
        }
        
        if (index == 0) {
            if (this.head.next != null) {
                this.head.next.prev = null;
            }
            
            this.head = this.head.next;
            //print();
            return;
        }
        
        int i = 0;
        Node prev = this.head;
        while (i < index - 1 && prev != null) {
            prev = prev.next;
            i++;
        }
        if (prev == null || prev.next == null) {
            //print();
            return;
        }
        
        if (prev.next.next != null) {
            prev.next.next.prev = prev;
        }
        prev.next = prev.next.next;

        //print();
    }
    
    // private void print() {
    //     Node curr = this.head;
    //     while (curr != null) {
    //         System.out.print(curr.val);
    //         curr = curr.next;
    //     }
    //     System.out.println("---");
    // }
    
}

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.get(index);
 * obj.addAtHead(val);
 * obj.addAtTail(val);
 * obj.addAtIndex(index,val);
 * obj.deleteAtIndex(index);
 */
```



## 141 [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle)    

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */

// public class Solution {
//     public boolean hasCycle(ListNode head) {
//         ListNode slow = head;
//         ListNode fast = head;
//         boolean isMoved = false;
//         while (fast != null && (!isMoved || (isMoved && slow != fast))) {
//             isMoved = true;
//             if (fast.next == null) {
//                 fast = null;
//             } else {
//                 fast = fast.next.next;
//             }
//             slow = slow.next;
//         }
        
//         return fast != null;
//     }
// }

public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null) {
            return false;
        }
        
        ListNode slow = head;
        ListNode fast = head;
        do {
            if (fast.next == null) {
                fast = null;
            } else {
                fast = fast.next.next;
            }
            slow = slow.next;
            
        } while (fast != null && slow != fast);
        
        return fast != null;
    }
}


// public class Solution {
//     public boolean hasCycle(ListNode head) {
//         ListNode slow = head;
//         ListNode fast = head;
//         while (fast != null && fast.next != null) {
//             fast = fast.next.next;
//             slow = slow.next;
//             if (fast == slow) {
//                 break;
//             }
//         }
//         return fast == slow && fast != null && fast.next != null;
//     }
// }


// public class Solution {
//     public boolean hasCycle(ListNode head) {
//         ListNode slow = head;
//         ListNode fast = head;
//         while (fast != null && fast.next != null) {
//             slow = slow.next;
//             fast = fast.next.next;
//             if (slow == fast) {
//                 return true;
//             }
//         }
//         return false;
//     }
// }
```





## 142 [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii)    

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
// public class Solution {
//     public ListNode detectCycle(ListNode head) {
//         ListNode slow = head;
//         ListNode fast = head;
//         boolean isMoved = false;
//         while (fast != null && (!isMoved || (isMoved && slow != fast))) {
//             if (isMoved == false) {
//                 isMoved = true;
//             }
            
//             if (fast.next == null) {
//                 fast = null;
//             } else {
//                 fast = fast.next.next;
//             }
//             slow = slow.next;
//         }
        
//         if (fast == null) {
//             return null;
//         }
        
//         fast = head;
//         while (slow != fast) {
//             fast = fast.next;
//             slow = slow.next;
//         }
//         return fast;
//     }
// }


// public class Solution {
//     public ListNode detectCycle(ListNode head) {
        
//         ListNode slow = head;
//         ListNode fast = head;
//         while (fast != null && fast.next != null) {
//             fast = fast.next.next;
//             slow = slow.next;
//             if (fast == slow) {
//                 break;
//             }
//         }
        
//         if (!(fast == slow && fast != null && fast.next != null)) {
//             return null;
//         }
        
//         fast = head;
//         while (slow != fast) {
//             fast = fast.next;
//             slow = slow.next;
//         }
//         return fast;
//     }
// }


public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) {
                fast = head;
                while (slow != fast) {
                    fast = fast.next;
                    slow = slow.next;
                }
                return fast;
            }
        }
        return null;
    }
}
```







## 160 [Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists) 

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }
   
        ListNode a = headA;
        while (a.next != null) {
            a = a.next;
        }
        a.next = headA;
        
        // return detectCycle(headB, a);
        ListNode res = detectCycle(headB);
        a.next = null;
        return res;
    }
    
    private ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) {
                fast = head;
                while (slow != fast) {
                    fast = fast.next;
                    slow = slow.next;
                }
                return fast;
            }
        }
        return null;
    }
}


// public class Solution {
    
//     public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
//         if (headA == null || headB == null) {
//             return null;
//         }
        
//         ListNode a = headA;
//         ListNode b = headB;
//         while (a != b) {
//             a = a == null ? headB: a.next;
//             b = b == null ? headA: b.next;
//         }
//         return a;
//     }
// }


// public class Solution {
    
//     public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
//         if (headA == null || headB == null) {
//             return null;
//         }
        
//         ListNode a = headA;
//         ListNode b = headB;
//         while (a != b) {
//             a = a.next;
//             b = b.next;
//             if (a == b) {
//                 return a;
//             }
//             if (a == null) {
//                 a = headB;
//             }
//             if (b == null) {
//                 b = headA;
//             }
//         }
//         return a;
//     }
// }
```





## 19 [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list)    

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
    
// class Solution {
//     public ListNode removeNthFromEnd(ListNode head, int n) {
//         if (head == null) {
//             return null;
//         }
//         int len = getLen(head);
//         int index = len - n;
        
//         // remove 1st one
//         if (index == 0) {
//             return head.next;
//         }
        
//         ListNode pre = head;
//         int i = 0;
//         while (i < index - 1) {
//             pre = pre.next;
//             i++;
//         }
        
//         pre.next = pre.next.next;
//         return head;
//     }
    
//     private int getLen(ListNode head) {
//         ListNode curr = head;
//         int res = 0;
//         while (curr != null) {
//             curr = curr.next;
//             res++;
//         }
//         return res;
//     }
// }
    

// 2
// 1 2 3 4 5

// 1
    
// class Solution {
//     public ListNode removeNthFromEnd(ListNode head, int n) {
//         if (head == null) {
//             return null;
//         }
        
//         ListNode start = new ListNode(0);
//         start.next = head;
//         ListNode fast = start, slow = start;
        
//         for (int i = 0; i < n; i++) {
//             fast = fast.next;
//         }
        
//         if (fast.next == null) {
//             return head.next;
//         }
        
//         while (fast.next != null) {
//             fast = fast.next;
//             slow = slow.next;
//         }
//         slow.next = slow.next.next;
//         return head;
//     }
// }


// 1
// 1

class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) {
            return null;
        }
        
        ListNode start = new ListNode(0);
        start.next = head;
        ListNode fast = start, slow = start;

        for (int i = 0; i < n; i++) {
            fast = fast.next;
        }
        
        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }
        slow.next = slow.next.next;
        
        return start.next;
    }
}
```





## 206 [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list)     

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
//     public ListNode reverseList(ListNode head) {
//         if (head == null) {
//             return head;
//         }
        
//         ListNode h = head;
//         ListNode pre = head;
//         ListNode curr = head.next;
        
//         while (curr != null) {
//             pre.next = curr.next;
//             curr.next = h;
            
//             h = curr;
//             curr = pre.next;
//         }
//         return h;
//     }
    
    
//     public ListNode reverseList(ListNode head) {
//         if (head == null) {
//             return head;
//         }
        
//         ListNode h = head;
//         ListNode curr = head.next;

//         while (curr != null) {
//             head.next = curr.next;
//             curr.next = h;
            
//             h = curr;
//             curr = head.next;
//         }
//         return h;
//     }
    
//     public ListNode reverseList(ListNode head) {
//         if (head == null) {
//             return head;
//         }
        
//         ListNode h = head;
        

//         while (head.next != null) {
//             ListNode curr = head.next;
//             head.next = curr.next;
//             curr.next = h;
//             h = curr;
//         }
//         return h;
//     }
    
    
    // recursion
//     public ListNode reverseList(ListNode head) {
//         // if (head == null) {
//         //     return null;
//         // }
//         // if (head.next == null) {
//         //     return head;
//         // }
        
//         if (head == null || head.next == null) {
//             return head;
//         }
//         ListNode newHead = reverseList(head.next);
        
//         // ListNode curr = newHead;
//         // while (curr.next != null) {
//         //     curr = curr.next;
//         // }
//         // curr.next = head;
        
//         // head.next = curr!!!!!!
//         head.next.next = head;
        
//         head.next = null;
//         return newHead;
//     }
    
    
    // iteration
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        
        // ListNode prev = head;
        // ListNode curr = prev.next;
        // prev.next = null;
        
        ListNode prev = null;
        ListNode curr = head;
        
        while (curr != null) {
            ListNode temp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = temp;
        }
        return prev;
    }
}
```





## 203 [Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements)  

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    //method1: dummyNode
//     public ListNode removeElements(ListNode head, int val) {
//         ListNode dummyNode = new ListNode(-1);
//         dummyNode.next = head;
        
//         ListNode pre = dummyNode;
        
//         while (pre.next != null) {
//             if (pre.next.val != val) {
//                 pre = pre.next;
//             } else {
//                 pre.next = pre.next.next;
//             }
//         }
        
//         return dummyNode.next;
//     }
    
    //method2: w/t dummyNode
    public ListNode removeElements(ListNode head, int val) {
        while (head != null && head.val == val) {
            head = head.next;
        }
        if (head == null) {return null;}
        
        ListNode pre = head;
        while (pre.next != null) {
            if (pre.next.val == val) {
                pre.next = pre.next.next;
            } else {
                pre = pre.next;
            }
        }
        
        return head;
    }
    
    
    //method3: recursion
    // public ListNode removeElements(ListNode head, int val) {
    //     if (head == null) {
    //         return null;
    //     }
    //     head.next = removeElements(head.next, val);
    //     return head.val == val ? head.next : head;
    // }
}
```





## 328 [Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list)    

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if (head == null || head.next == null || head.next.next == null) {
            return head;
        }
        
        ListNode odd = head;
        ListNode even = head.next;
        
        ListNode p = even;
        
        //Memory Limit Exceed
//         while (odd != null && odd.next != null && odd.next.next != null) {
//             odd.next = odd.next.next;
//             odd = odd.next;
//         }
        
//         while (even != null && even.next != null && even.next.next != null) {
//             even.next = even.next.next;
//             even = even.next;
//         }
        
        while (even != null && even.next != null) {
            odd.next = odd.next.next;
            odd = odd.next;
            even.next = even.next.next;
            even = even.next;
        }
        
        odd.next = p;
        
        return head;
    }
}
```



## 234 [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list)    

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }
        ListNode fast = head, slow = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next; 
            slow = slow.next;
        }
        // System.out.println(slow.val);
        ListNode reverse = reverse(slow);
        fast = head;
        
        while (fast!= null && reverse != null) {
            if (fast.val != reverse.val) {
                return false;
            }
            fast = fast.next;
            reverse = reverse.next;
        }
        return true;
    }
    
    private ListNode reverse(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode currHead = head;
        ListNode curr = head.next;
        while (head.next != null) {
            head.next = curr.next;
            curr.next = currHead;
            currHead = curr;
            curr = head.next;
        }
        return currHead;
    }
}
```



## 707 [Design Linked List](https://leetcode.com/problems/design-linked-list)   

```java
class MyLinkedList {
    private Node head;
    
    private class Node {
        int val;
        Node next;
        Node prev;
        
        Node(int val) {
            this.val = val;
            // this.next = null;
            // this.prev = null;
        }
        Node() {
            // this.next = null;
        }
    }

    
    /** Initialize your data structure here. */
    public MyLinkedList() {
        Node head = new Node();
        // Node head = null;
    }
    
    /** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
    public int get(int index) {
        int i = 0;
        Node curr = head;
        while (i < index && curr != null) {
            curr = curr.next;
            i++;
        }
        if (curr == null) {
            //print();
            return -1;
        }
        //print();
        return curr.val;
        
    }
    
    /** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
    public void addAtHead(int val) {
        Node newHead = new Node(val);
        
        if (this.head != null) {
            this.head.prev = newHead;
        }
        newHead.next = this.head;
        
        this.head = newHead;
        //print();
    }
    
    /** Append a node of value val to the last element of the linked list. */
    public void addAtTail(int val) {
        if (this.head == null) {
            this.head = new Node(val);
            //print();
            return;
        }
        Node curr = this.head;
        while (curr.next != null) {
            curr = curr.next;
        }
        Node last = new Node(val);
        last.prev = curr;
        curr.next = last;
        //print();
    }
    
    /** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
    public void addAtIndex(int index, int val) {
        if (index == 0) {
            
            Node newHead = new Node(val);
            if (this.head != null) {
                this.head.prev = newHead;
            }
            newHead.next = this.head;
            
            this.head = newHead;
            
            //print();
            return;
        }
        
        int i = 0;
        Node prev = this.head;
        while (i < index - 1 && prev != null) {
            prev = prev.next;
            i++;
        }

        if (prev == null) {
            //print();
            return;
        }
        Node insertNode = new Node(val);
        
        insertNode.next = prev.next;
        insertNode.prev = prev;
        
        if (prev.next != null) {
            prev.next.prev = insertNode;  
        }
        prev.next = insertNode;
 
        //print();
    }
    
    /** Delete the index-th node in the linked list, if the index is valid. */
    public void deleteAtIndex(int index) {
        if (this.head == null) {
            //print();
            return;
        }
        
        if (index == 0) {
            if (this.head.next != null) {
                this.head.next.prev = null;
            }
            
            this.head = this.head.next;
            //print();
            return;
        }
        
        int i = 0;
        Node prev = this.head;
        while (i < index - 1 && prev != null) {
            prev = prev.next;
            i++;
        }
        if (prev == null || prev.next == null) {
            //print();
            return;
        }
        
        if (prev.next.next != null) {
            prev.next.next.prev = prev;
        }
        prev.next = prev.next.next;

        //print();
    }
    
    // private void print() {
    //     Node curr = this.head;
    //     while (curr != null) {
    //         System.out.print(curr.val);
    //         curr = curr.next;
    //     }
    //     System.out.println("---");
    // }
    
}

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList obj = new MyLinkedList();
 * int param_1 = obj.get(index);
 * obj.addAtHead(val);
 * obj.addAtTail(val);
 * obj.addAtIndex(index,val);
 * obj.deleteAtIndex(index);
 */
```





## 21 [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists)   

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    //merge l1 and l2 交叉
//     public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
//         if (l1 == null) {
//             return l2;
//         }
//         if (l2 == null) {
//             return l1;
//         }
        
//         ListNode l1cur = l1;
//         ListNode l1aft = l1.next;
//         ListNode l2cur = l2;
//         ListNode l2aft = l2.next;
//         while (l1cur != null && l2cur != null) {
//             l1cur.next = l2cur;
//             l1cur = l1aft;
//             if (l1aft != null) {
//                 l1aft = l1aft.next;
//             }
//             l2cur.next = l1cur;
//             l2cur = l2aft;
//             if (l2aft != null) {
//                 l2aft = l2aft.next;
//             }
//         }
//         return l1;
//     }
    
//     public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
//         if (l1 == null) {
//             return l2;
//         }
//         if (l2 == null) {
//             return l1;
//         }
        
//         ListNode res = l1.val <= l2.val ? l1 : l2;
        
//         ListNode cur = res;
//         ListNode cur1 = l1;
//         ListNode cur2 = l2;
//         if (l1.val <= l2.val) {
//             cur1 = cur1.next;
//         } else {
//             cur2 = cur2.next;
//         }
        
//         while (cur1 != null && cur2 != null) {
//             if (cur1.val <= cur2.val) {
//                 cur.next = cur1;
//                 cur1 = cur1.next;
//             }
//             else {
//                 cur.next = cur2;
//                 cur2 = cur2.next;
//             }
//             cur = cur.next;
//         }
        
//         cur.next = cur1 == null ? cur2 : cur1;
//         return res;
//     }
    
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) { 
            return l1;
        }
        if (l1.val <= l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        }
        else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}
```



## 2 [Add Two Numbers](https://leetcode.com/problems/add-two-numbers)   

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int sum = 0;
        ListNode dummyNode = new ListNode(-1);
        ListNode d = dummyNode;
        while (l1 != null || l2 != null) {
            sum /= 10;
            if (l1 != null) {
                sum += l1.val;
                l1 = l1.next;
            }
            if (l2 != null) {
                sum += l2.val;
                l2 = l2.next;
            }
            d.next = new ListNode(sum % 10);
            d = d.next;
        }
        if (sum / 10 == 1) {
            d.next = new ListNode(1);
        }
        return dummyNode.next;
    }
}
```





## 430 [Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list)    

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node prev;
    public Node next;
    public Node child;

    public Node() {}

    public Node(int _val,Node _prev,Node _next,Node _child) {
        val = _val;
        prev = _prev;
        next = _next;
        child = _child;
    }
};
*/
// class Solution {
//     public Node flatten(Node head) {
//         flattentail(head);
//         return head;
//     }
    
//     private Node flattentail(Node head) {
//         if (head == null) { // case1: head = null 
//             return null;
//         }
        
//         Node child = head.child;
//         Node next = head.next;
        
//         if (child == null) {
//             if (next == null) {
//                 return head; // case2: child = null, next = null
//             }
//             return flattentail(next); // case3: child = null, next != null
//         }
        
        
//         Node childNodeTail = flattentail(child);
        
//         // make sure head.child = null!!!!!!!!!!!!
//         head.child = null;
        
//         head.next = child;
//         child.prev = head;
        
//         // how about childNodeTail = null? is that possible?
//         childNodeTail.next = next;
        
//         if (next == null) { 
//             return childNodeTail; // case4: child != null, next == null
//         }
//         next.prev = childNodeTail;
//         return flattentail(next); // case5: child != null, next != null
//     }
// }



class Solution {
    public Node flatten(Node head) {
        if (head == null) { 
            return null;
        }

        Node curr = head;
        while (curr != null) {
            
            if (curr.child == null) {
                curr = curr.next;
                continue;
            }
            Node childTail = curr.child;
            
            while (childTail.next != null) {
                childTail = childTail.next;
            }
            
            childTail.next = curr.next;
            
            if (curr.next != null) {
                curr.next.prev = childTail;
            }
            
            curr.next = curr.child;
            curr.child.prev = curr;
            
            curr.child = null;
        }
        
        return head;
    }

}
```



## 708 [Insert into a Cyclic Sorted List](https://leetcode.com/problems/insert-into-a-cyclic-sorted-list)   

```java
// /*
// // Definition for a Node.
// class Node {
//     public int val;
//     public Node next;

//     public Node() {}

//     public Node(int _val,Node _next) {
//         val = _val;
//         next = _next;
//     }
// };
// */
// class Solution {
//     public Node insert(Node head, int insertVal) {
//         //null
//         if (head == null) {
//             Node res = new Node(insertVal);
//             res.next = res;
//             return res;
//         }
        
//         Node curr = head;
//         while (true) {
//             //case1 tipping point  => max, min  
//             //case1A  curr.val <= X <= curr.next.val
//             if (curr.val < curr.next.val) {
//                 if (curr.val <= insertVal && insertVal <= curr.next.val) {
//                     insertAfter(curr, insertVal);
//                     break;
//                 }
//             }
//             //case1B  x <= max or x >= min
//             else if (curr.val > curr.next.val) {
//                 if (insertVal >= curr.val || insertVal <= curr.next.val) {
//                     insertAfter(curr, insertVal);
//                     break;
//                 }
//             }
//             else {
//                 //case2 no tipping point!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
//                 if (curr.next == head) {
//                     insertAfter(curr, insertVal);
//                     break;
//                 }
//             }
//             curr = curr.next;
//         }
//         return head;
//     }
    
//     private void insertAfter (Node head, int insertVal) {
//         head.next = new Node(insertVal, head.next);
//     }
// }




class Solution {
    public Node insert(Node start, int x) {
        // if start is null, create a node pointing to itself and return
        if (start == null) {
            Node node = new Node(x, null);
            node.next = node;
            return node;
        }
        // first pass to find max node 
        Node curr = start;
        while (curr.val <= curr.next.val && curr.next != start) {
            curr = curr.next;
        }
        
        Node max = curr;
        //dummyNode.next = min node
        Node dummyNode = new Node(0, max.next);
        max.next = null;
        
        curr = dummyNode;
        while (curr.next != null && x > curr.next.val) {
            curr = curr.next;
        }
        curr.next = new Node(x, curr.next);
        
        //update max node
        if (max.next != null) {
            max = max.next;
        }
        max.next = dummyNode.next;
        
        return start;
    }
}
```







## 138 [Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer)   

```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
// public class Solution {
//     // original RandomListNode => copy RandomListNode
//     Map<RandomListNode, RandomListNode> map = new HashMap();
    
//     public RandomListNode copyRandomList(RandomListNode head) {
//         if (head == null) {
//             return null;
//         }
        
//         //if map contains copyed head, use copyed head
//         if (this.map.containsKey(head)) {
//             return this.map.get(head);
//         }
        
//         //if map doesn't contain copyed head, create new one
//         RandomListNode copyHead = new RandomListNode(head.label);
//         this.map.put(head, copyHead);
        
//         //copy next and random
//         copyHead.next = copyRandomList(head.next);
//         copyHead.random = copyRandomList(head.random);
//         return copyHead;
//     }
// }






// public class Solution {
//     public RandomListNode copyRandomList(RandomListNode head) {
//         if (head == null) {
//             return null;
//         }
        
//         // original RandomListNode => copy RandomListNode
//         Map<RandomListNode, RandomListNode> map = new HashMap();
        
        
//         RandomListNode copyHead = new RandomListNode(head.label);
//         map.put(head, copyHead);
        
//         RandomListNode curr = head;
//         RandomListNode copyCurr = copyHead;
        
//         while (curr != null) {
//             if (curr.next == null) {
//                 copyCurr.next = null;
//             } else {
//                 RandomListNode copyNext = new RandomListNode(curr.next.label);
//                 map.put(curr.next, copyNext);
//                 copyCurr.next = copyNext;
//             }

            
//             //if map doesn't contain copyed random, create new one
//             if (!map.containsKey(curr.random)) {
//                 if (curr.random == null) {
//                     copyCurr.random = null;
//                 } else {
//                     RandomListNode copyRandom = new RandomListNode(curr.random.label);
//                     map.put(curr.random, copyRandom);
//                     copyCurr.random = copyRandom;
//                 }

//             }
//             //if map contains copyed copyed random, use copyed curr
//             else {
//                 copyCurr.random = map.get(curr.random);
//             }
//             curr = curr.next;
//             copyCurr = copyCurr.next;
//         }
//         return copyHead;
//     }
// }



// public class Solution {
//     private RandomListNode getCloneRandomListNode(RandomListNode head, Map<RandomListNode, RandomListNode> map) {
//         if (head == null) {
//             return null;
//         }
//         //if map doesn't contain copyed head, create new one
//         if (!map.containsKey(head)) {
//             RandomListNode copy = new RandomListNode(head.label);
//             map.put(head, copy);
//             return copy;
//         }
//         //if map contains copyed copyed head, use copyed curr
//         else {
//             return map.get(head);
//         }
//     }
    
//     public RandomListNode copyRandomList(RandomListNode head) {
//         if (head == null) {
//             return null;
//         }
        
//         // original RandomListNode => copy RandomListNode
//         Map<RandomListNode, RandomListNode> map = new HashMap();
        
//         RandomListNode copyHead = new RandomListNode(head.label);
//         map.put(head, copyHead);
//         RandomListNode curr = head;
        
//         // RandomListNode copyCurr = copyHead;
//         // while (curr != null) {
//         //     copyCurr.next = getCloneRandomListNode(curr.next, map);
//         //     copyCurr.random = getCloneRandomListNode(curr.random, map);
//         //     curr = curr.next;
//         //     copyCurr = copyCurr.next;
//         // }
//         // return copyHead;
        
        
//         while (curr != null) {
//             copyHead.next = getCloneRandomListNode(curr.next, map);
//             copyHead.random = getCloneRandomListNode(curr.random, map);
//             curr = curr.next;
//             copyHead = copyHead.next;
//         }
//         return map.get(head);
//     }
// }



public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) {
            return null;
        }

        RandomListNode curr = head;
        
        //copy node
        while (curr != null) {
            RandomListNode copy = new RandomListNode(curr.label);
            copy.next = curr.next;
            curr.next = copy;
            
            //curr = curr.next.next;
            curr = copy.next;
        }
        curr = head;
        
        //copy random
        //while (curr != null && curr.next != null) {
        while (curr != null) {
            curr.next.random = curr.random == null ? null : curr.random.next;
            curr = curr.next.next;
        }
        
        //copy next
        curr = head;
        RandomListNode copyHead = head.next;
        RandomListNode currCopy = copyHead;
        
        // while (currCopy != null) {
        //     curr.next = currCopy.next;
        //     curr = curr.next;
        //     if (curr == null) {
        //         break;
        //     }
        //     currCopy.next = curr.next;
        //     currCopy = currCopy.next;
        // }
        
        while (currCopy != null) {
            curr.next = currCopy.next;
            curr = curr.next;
 
            currCopy.next = curr == null ? null : curr.next;
            currCopy = currCopy.next;
        }
        
        return copyHead;
    }
}
```





## 61 [Rotate List](https://leetcode.com/problems/rotate-list) 

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
// class Solution {
//     public ListNode rotateRight(ListNode head, int k) {
//         if (head == null || head.next == null) {
//             return head;
//         }
//         int len = getLen(head);
//         // if (k % len == 0) {
//         //     return head;
//         // }
        
//         int pos = len - k % len;
//         ListNode[] nodeArr = getNodeAtPos(head, pos - 1);
//         ListNode pre = nodeArr[0];
//         ListNode tail = nodeArr[1];
//         tail.next = head;
//         ListNode newHead = pre.next;
//         pre.next = null;
//         return newHead;
//     }
    
//     private int getLen(ListNode head) {
//         ListNode curr = head;
//         int res = 0;
//         while (curr != null) {
//             curr = curr.next;
//             res++;
//         }
//         return res;
//     }
    
//     //get node at pos and tail
//     private ListNode[] getNodeAtPos(ListNode head, int pos) {
//         int i = 0;
//         ListNode curr = head;
//         ListNode[] res = new ListNode[2];
//         while (i < pos) {
//             curr = curr.next;
//             i++;
//         }
//         res[0] = curr;
//         while (curr != null && curr.next != null) {
//             curr = curr.next;
//         }
//         res[1] = curr;
//         return res;
//     }
// }

// class Solution {
//     public ListNode rotateRight(ListNode head, int k) {
//         if (head == null || head.next == null) {
//             return head;
//         }
        
        
//         int len = 1;
//         ListNode tail = head;
//         while (tail.next != null) {
//             tail = tail.next;
//             len++;
//         }
        
//         // if (k % len == 0) {
//         //     return head;
//         // }
        
//         int pos = len - k % len;
//         ListNode pre = getNodeAtPos(head, pos - 1);
        
//         //if pre is the last node, tail.next = head => pre.next = head;
//         tail.next = head;
//         ListNode newHead = pre.next;
//         pre.next = null;
//         return newHead;
//     }

//     //get node at pos
//     private ListNode getNodeAtPos(ListNode head, int pos) {
//         int i = 0;
//         ListNode curr = head;
//         while (i < pos) {
//             curr = curr.next;
//             i++;
//         }
//         return curr;
//     }
// }


class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode dummyNode = new ListNode(0);
        dummyNode.next = head;
        
        int len = 0;
        ListNode tail = dummyNode;
        while (tail.next != null) {
            tail = tail.next;
            len++;
        }
        
        // if (k % len == 0) {
        //     return head;
        // }
        
        int pos = len - k % len;
        //ListNode pre = getNodeAtPos(head, pos - 1);
        // (head, pos - 1) = (dummyNode, pos)
        ListNode pre = getNodeAtPos(dummyNode, pos);
        
        //if pre is the last node, tail.next = head => pre.next = head;
        tail.next = head;
        dummyNode.next = pre.next;
        pre.next = null;
        return dummyNode.next;
    }

    //get node at pos
    private ListNode getNodeAtPos(ListNode head, int pos) {
        int i = 0;
        ListNode curr = head;
        while (i < pos) {
            curr = curr.next;
            i++;
        }
        return curr;
    }
}

// class Solution {
//     public ListNode rotateRight(ListNode head, int n) {
//         if (head==null||head.next==null) return head;
//         ListNode dummy=new ListNode(0);
//         dummy.next=head;
//         ListNode fast=dummy,slow=dummy;

//         int i;
//         for (i=0;fast.next!=null;i++)//Get the total length 
//             fast=fast.next;

//         for (int j=i-n%i;j>0;j--) //Get the i-n%i th node
//             slow=slow.next;
     
//         fast.next=dummy.next; //Do the rotation
//         dummy.next=slow.next;
//         slow.next=null;

//         return dummy.next;
//     }
// }
```



