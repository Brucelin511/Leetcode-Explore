## 704 [Binary Search](https://leetcode.com/problems/binary-search)   

```java
class Solution {
    // public int search(int[] nums, int target) {
    //     int left = 0;
    //     int right = nums.length - 1;
    //     while (left <= right) {
    //         int middle = left + (right - left) / 2;
    //         if (nums[middle] < target) {
    //             left = middle + 1;
    //         } 
    //         else if (nums[middle] > target) {
    //             right = middle - 1;
    //         }
    //         else {
    //             return middle;
    //         }
    //     }
    //     return -1;
    // }
    
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int left = 0;
        int right = nums.length - 1;
        while (left + 1 < right) {
            int middle = left + (right - left) / 2;
            if (nums[middle] < target) {
                left = middle;
            } 
            else if (nums[middle] > target) {
                right = middle;
            }
            else {
                return middle;
            }
        }
        if (nums[left] == target) {
            return left;
        }
        if (nums[right] == target) {
            return right;
        }
        return -1;
    }
}
```



## 69 [Sqrt(x)](https://leetcode.com/problems/sqrtx)    

```java
class Solution {
    
    //version 1
    // public int mySqrt(int x) {
    //     if (x == 0) {
    //         return 0;
    //     }
    //     int left = 1;
    //     int right = x;
    //     while (left <= right) {
    //         int middle = left + (right - left) / 2;
    //         if (middle < x / middle) {
    //             left = middle + 1;
    //         }
    //         else if (middle > x / middle) {
    //             right = middle - 1;
    //         }
    //         else {
    //             return middle;
    //         }
    //     }
    //     return right;
    // }
    
    
    //version 2
    public int mySqrt(int x) {
        if (x == 0) {
            return 0;
        }
        int left = 1;
        int right = x;
        while (left + 1 < right) {
            int middle = left + (right - left) / 2;
            if (middle < x / middle) {
                left = middle;
            }
            else if (middle > x / middle) {
                right = middle;
            }
            else {
                return middle;
            }
        }
        if (right < x / right) {
            return right;
        }
        return left;
    }
}
```





## 374 [Guess Number Higher or Lower](https://leetcode.com/problems/guess-number-higher-or-lower)    

```java
/* The guess API is defined in the parent class GuessGame.
   @param num, your guess
   @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
      int guess(int num); */

public class Solution extends GuessGame {
    // public int guessNumber(int n) {
    //     int left = 1;
    //     int right = n;
    //     while (true) {
    //         int middle = left + (right - left) / 2;
    //         int api = guess(middle);
    //         if (api == -1) {
    //             right = middle - 1;
    //         }
    //         else if (api == 1) {
    //             left = middle + 1;
    //         }
    //         else if (api == 0) {
    //             return middle;
    //         }
    //     }
    // }
    
    //version2
    // public int guessNumber(int n) {
    //     int i = 1, j = n;
    //     while(i < j) {
    //         int mid = i + (j - i) / 2;
    //         if(guess(mid) == 0) {
    //             return mid;
    //         } else if(guess(mid) == 1) {
    //             i = mid + 1;
    //         } else {
    //             j = mid - 1;
    //         }
    //     }
    //     return i;
    // }
    
    public int guessNumber(int n) {
        int left = 1;
        int right = n;
        while (left + 1 < right) {
            int middle = left + (right - left) / 2;
            int api = guess(middle);
            if (api == -1) {
                right = middle;
            }
            else if (api == 1) {
                left = middle;
            }
            else if (api == 0) {
                return middle;
            }
        }
        if (guess(left) == 0) {
            return left;
        }
        return right;
    }
}
```







## 33 [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array)     

```java
class Solution {
    
//     //verion 1
//     public int search(int[] nums, int target) {

//         if (nums == null || nums.length == 0) {
//             return -1;
//         }
//         int left = 0;
//         int right = nums.length - 1;

        
//         while (left <= right) {
//             int middle = left + (right - left) / 2;
//             int value = nums[middle];
//             if (value <= nums[right]) {
//                 if (value > target) {
//                     right = middle - 1;
//                 }
//                 else if (value < target) {
//                     if (target <= nums[right]) {
//                         left = middle + 1;
//                     } else {
//                         right = middle - 1;
//                     }
//                 }
//                 else {
//                     return middle;
//                 }
//             }
//             else if (value > nums[right]) {
//                 if (value > target) {
//                     if (target <= nums[right]) {
//                         left = middle + 1;
//                     } else {
//                         right = middle - 1;
//                     }
//                 } 
//                 else if (value < target) {
//                     left = middle + 1;
//                 }
//                 else {
//                     return middle;
//                 }
//             }
//         }
//         return -1;
//     }
    
//         //verion 2
//     public int search(int[] nums, int target) {
//         if (nums == null || nums.length == 0) {
//             return -1;
//         }
        
//         int left = 0;
//         int right = nums.length - 1;
//         while (left < right) {
//             int middle = left + (right - left) / 2;
//             int value = nums[middle];
//             if (value <= nums[right]) {
//                 if (value > target) {
//                     right = middle - 1;
//                 }
//                 else if (value < target) {
//                     if (target <= nums[right]) {
//                         left = middle + 1;
//                     } else {
//                         right = middle - 1;
//                     }
//                 }
//                 else {
//                     return middle;
//                 }
//             }
//             else if (value > nums[right]) {
//                 if (value > target) {
//                     if (target <= nums[right]) {
//                         left = middle + 1;
//                     } else {
//                         right = middle - 1;
//                     }
//                 } 
//                 else if (value < target) {
//                     left = middle + 1;
//                 }
//                 else {
//                     return middle;
//                 }
//             }
//         }
//         if (nums[left] == target) {
//             return left;
//         }
//         return -1;
//     }
    
    
            //verion 3
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int left = 0;
        int right = nums.length - 1;
        while (left + 1 < right) {
            int middle = left + (right - left) / 2;
            int value = nums[middle];
            if (value <= nums[right]) {
                if (value > target) {
                    right = middle - 1;
                }
                else if (value < target) {
                    if (target <= nums[right]) {
                        left = middle + 1;
                    } else {
                        right = middle - 1;
                    }
                }
                else {
                    return middle;
                }
            }
            else if (value > nums[right]) {
                if (value > target) {
                    if (target <= nums[right]) {
                        left = middle + 1;
                    } else {
                        right = middle - 1;
                    }
                } 
                else if (value < target) {
                    left = middle + 1;
                }
                else {
                    return middle;
                }
            }
        }
        if (nums[left] == target) {
            return left;
        }
        if (nums[right] == target) {
            return right;
        }
        return -1;
    }
    

}
```



## 278 [First Bad Version](https://leetcode.com/problems/first-bad-version)   

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    // public int firstBadVersion(int n) {
    //     int left = 1;
    //     int right = n;
    //     while (left + 1 < right) {
    //         int middle = left + (right - left) / 2;
    //         boolean isBad = isBadVersion(middle);
    //         if (isBad == false) {
    //             left = middle;
    //         } else {
    //             right = middle;
    //         }
    //     }
    //     if (isBadVersion(left)) {
    //         return left;
    //     }
    //     if (isBadVersion(right)) {
    //         return right;
    //     }
    //     return -1;
    // }
    
    public int firstBadVersion(int n) {
        int left = 1;
        int right = n;
        while (left < right) {
            int middle = left + (right - left) / 2;
            boolean isBad = isBadVersion(middle);
            if (isBad == false) {
                left = middle + 1;
            } else {
                right = middle;
            }
        }
        if (isBadVersion(left)) {
            return left;
        }
        return -1;
    }
}
```



## 162 [Find Peak Element](https://leetcode.com/problems/find-peak-element)    

```java
class Solution {
    // public int findPeakElement(int[] nums) {
    //     int left = 0;
    //     int right = nums.length - 1;
    //     while (left < right) {
    //         int middle = left + (right - left) / 2;
    //         if (nums[middle] < nums[middle + 1]) {
    //             left = middle + 1;
    //         } else {
    //             right = middle;
    //         }
    //     }
    //     return left;
    // }
    
    public int findPeakElement(int[] nums) {
        
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int left = 0;
        int right = nums.length - 1;
        while (left + 1 < right) {
            int middle = left + (right - left) / 2;
            if (nums[middle] < nums[middle + 1]) {
                left = middle;
            } else {
                right = middle;
            }
        }
        if (nums[left] > nums[right]) {
            return left;
        }
        return right;
    }
    
    
    
    // public int findPeakElement(int[] nums) {
    //     int left = 0;
    //     int right = nums.length - 1;
    //     while (left + 1 < right) {
    //         int middle = left + (right - left) / 2;
    //         if (nums[middle - 1] < nums[middle] && nums[middle] > nums[middle + 1]) {
    //             return middle;
    //         }
    //         else if (nums[middle - 1] < nums[middle] && nums[middle] < nums[middle + 1]) {
    //             left = middle;
    //         }
    //         else if (nums[middle - 1] > nums[middle] && nums[middle] > nums[middle + 1]) {
    //             right = middle;
    //         }
    //         else if (nums[middle - 1] > nums[middle] && nums[middle] < nums[middle + 1]) {
    //             right = middle;
    //         }
    //     }
    //     if (nums[left] > nums[right]) {
    //         return left;
    //     }
    //     return right;
    // }
}
```





## 153 [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array)    

```java
class Solution {
    
    // public int findMin(int[] nums) {
    //     if (nums == null || nums.length == 0) {
    //         return -1;
    //     }
    //     int left = 0;
    //     int right = nums.length - 1;
    //     while (left < right) {
    //         if (nums[left] < nums[right]) {
    //             return nums[left];
    //         }
    //         int middle = left + (right - left) / 2;
    //         if (nums[middle] > nums[left]) {
    //             left = middle + 1;
    //         }
    //         else if (nums[middle] == nums[left]) {
    //             left = middle + 1;
    //         }
    //         else {
    //             right = middle;
    //         }
    //     }
    //     return nums[left];
    // }
    
    
//     public int findMin(int[] nums) {
//         if (nums == null || nums.length == 0) {
//             return -1;
//         }
//         int left = 0;
//         int right = nums.length - 1;
 
//         while (left < right) {
//             if (nums[left] < nums[right]) {
//                 return nums[left];
//             }
//             int middle = left + (right - left) / 2;
//             if (nums[middle] > nums[0]) {
//                 left = middle + 1;
//             }
//             else if (nums[middle] == nums[0]) {
//                 left = middle + 1;
//             }
//             else {
//                 right = middle;
//             }
//         }
//         return nums[left];
//     }
    
    public int findMin(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int last = nums[nums.length - 1];
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            if (nums[left] < nums[right]) {
                return nums[left];
            }
            int middle = left + (right - left) / 2;
            if (nums[middle] > last) {
                left = middle + 1;
            }
            else {
                right = middle;
            }
        }
        return nums[left];
    }
    
    // public int findMin(int[] nums) {
    //     if (nums == null || nums.length == 0) {
    //         return -1;
    //     }
    //     int last = nums[nums.length - 1];
    //     int left = 0;
    //     int right = nums.length - 1;
    //     while (left + 1 < right) {
    //         int middle = left + (right - left) / 2;
    //         if (nums[middle] > last) {
    //             left = middle;
    //         }
    //         else {
    //             right = middle;
    //         }
    //     }
    //     return nums[left] < nums[right] ? nums[left] : nums[right];
    // }
}
```





## [Search for a Range](https://leetcode.com/explore/learn/card/binary-search/135/template-iii/944/)   

```java
class Solution {
    
    public int[] searchRange(int[] nums, int target) {
        int[] result = {-1, -1};
        if (nums == null || nums.length == 0) {
            return result;
        }

        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            //left biased
            int middle = left + (right - left) / 2;
            if (nums[middle] < target) {
                left = middle + 1;
            }
            else {
                right = middle;
            }
        }
        if (nums[left] == target) {
            result[0] = left;
        }
        else {
            return result;
        }
        
        // left = 0;
        right = nums.length - 1;
        while (left < right) {
            //right biased
            int middle = right - (right - left) / 2;
            if (nums[middle] <= target) {
                left = middle;
            }
            else {
                right = middle - 1;
            }
        }
        if (nums[left] == target) {
            result[1] = left;
        }
        return result;
    }
    
//     public int[] searchRange(int[] nums, int target) {
//         int[] result = {-1, -1};
//         if (nums == null || nums.length == 0) {
//             return result;
//         }

//         int left = 0;
//         int right = nums.length - 1;
//         while (left + 1 < right) {
//             int middle = left + (right - left) / 2;
//             if (nums[middle] < target) {
//                 left = middle;
//             }
//             else {
//                 right = middle;
//             }
//         }
//         if (nums[left] == target) {
//             result[0] = left;
//         }
//         else if (nums[right] == target) {
//             result[0] = right;
//         }
//         else {
//             return result;
//         }
        
        
//         // left = 0;
//         right = nums.length - 1;
//         while (left + 1 < right) {
//             int middle = left + (right - left) / 2;
//             if (nums[middle] <= target) {
//                 left = middle;
//             }
//             else {
//                 right = middle;
//             }
//         }
//         if (nums[right] == target) {
//             result[1] = right;
//         }
//         else if (nums[left] == target) {
//             result[1] = left;
//         }
//         return result;
//     }
}
```





## 658 [Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements)

```java
class Solution {
//     public List<Integer> findClosestElements(int[] arr, int k, int x) {
//         if (arr == null || arr.length == 0) {
//             return null;
//         }
//         int left = 0;
//         int right = arr.length - 1;
//         int pos = -1;
//         while (left + 1 < right) {
//             int middle = left + (right - left) / 2;
//             if (arr[middle] > x) {
//                 right = middle;
//             }
//             else if (arr[middle] < x) {
//                 left = middle;
//             }
//             else {
//                 pos = middle;
//                 break;
//             }
//         }
//         if (pos == -1) {
//             pos = Math.abs(x - arr[left]) <= Math.abs(x - arr[right]) ? left : right;
//         }
        
//         left = pos;
//         right = pos;
//         while (right - left + 1 < k) {
//             if (left - 1 < 0) {
//                 right++;
//                 continue;
//             }
//             if (right + 1 >= arr.length) {
//                 left--;
//                 continue;
//             }
//             if (Math.abs(x - arr[left - 1]) <= Math.abs(x - arr[right + 1])) {
//                 left--;
//             } else {
//                 right++;
//             }
//         }
        
//         List<Integer> result = new LinkedList();
//         for (int i = left; i <= right; i++) {
//             result.add(arr[i]);
//         }
//         return result;
//         // return Arrays.stream(arr).boxed().collect(Collectors.toList()).subList(left, right + 1);
//     }
    
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        if (arr == null || arr.length == 0) {
            return null;
        }
        int left = 0, right = arr.length - k;
        
        while (left < right) {
            int middle = left + (right - left) / 2;
            
            //compare arr[middle] with arr[middle + k] not arr[middle + k - 1]
            // 2 3 3 4  arr[middle] = 2, k = 3
            // x = 3 then nums[left] ==> 2, x = 1 then nums[left] ==> 2, x = 5 then nums[right] ===> 4
            if (x - arr[middle] > arr[middle + k] - x) {
            // if (arr[middle] + arr[middle + k] < 2 * x) {
                left = middle + 1;
            }
            // else if (arr[middle] + arr[middle + k] > 2 * x) {
            else if (x - arr[middle] < arr[middle + k] - x) {
                right = middle;
            }
            else {
                right = middle;
            }
        }
        
        // while (left + 1 < right) {
        //     int middle = left + (right - left) / 2;
        //     if (x - arr[middle] > arr[middle + k] - x) {
        //     // if (arr[middle] + arr[middle + k] < 2 * x) {
        //         left = middle;
        //     }
        //     // else if (arr[middle] + arr[middle + k] > 2 * x) {
        //     else if (x - arr[middle] < arr[middle + k] - x) {
        //         right = middle;
        //     }
        //     else {
        //         right = middle;
        //     }
        // }
        
        List<Integer> result = new LinkedList();
        for (int i = left; i < left + k; i++) {
            result.add(arr[i]);
        }
        return result;
    }
}
```





## 162 [Find Peak Element](https://leetcode.com/problems/find-peak-element)

```java
class Solution {
    // public int findPeakElement(int[] nums) {
    //     int left = 0;
    //     int right = nums.length - 1;
    //     while (left < right) {
    //         int middle = left + (right - left) / 2;
    //         if (nums[middle] < nums[middle + 1]) {
    //             left = middle + 1;
    //         } else {
    //             right = middle;
    //         }
    //     }
    //     return left;
    // }
    
    public int findPeakElement(int[] nums) {
        
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int left = 0;
        int right = nums.length - 1;
        while (left + 1 < right) {
            int middle = left + (right - left) / 2;
            if (nums[middle] < nums[middle + 1]) {
                left = middle;
            } else {
                right = middle;
            }
        }
        if (nums[left] > nums[right]) {
            return left;
        }
        return right;
    }
    
    
    
    // public int findPeakElement(int[] nums) {
    //     int left = 0;
    //     int right = nums.length - 1;
    //     while (left + 1 < right) {
    //         int middle = left + (right - left) / 2;
    //         if (nums[middle - 1] < nums[middle] && nums[middle] > nums[middle + 1]) {
    //             return middle;
    //         }
    //         else if (nums[middle - 1] < nums[middle] && nums[middle] < nums[middle + 1]) {
    //             left = middle;
    //         }
    //         else if (nums[middle - 1] > nums[middle] && nums[middle] > nums[middle + 1]) {
    //             right = middle;
    //         }
    //         else if (nums[middle - 1] > nums[middle] && nums[middle] < nums[middle + 1]) {
    //             right = middle;
    //         }
    //     }
    //     if (nums[left] > nums[right]) {
    //         return left;
    //     }
    //     return right;
    // }
}
```



## 270 [Closest Binary Search Tree Value](https://leetcode.com/problems/closest-binary-search-tree-value)    

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
    
    
        // O(log(n)) recursion
//     public int closestValue(TreeNode root, double target) {
//         int a = root.val;
//         TreeNode kid = target < a ? root.left : root.right;
//         if (kid == null) {
//             return a;
//         }
//         int b = closestValue(kid, target);
        
//         return Math.abs(a - target) < Math.abs(b - target) ? a : b;
//     }
    
    // O(log(n)) iterative
    public int closestValue(TreeNode root, double target) {
        if (root == null) {
            throw new java.lang.Error("this is very bad");
        }
        
        int result = root.val;
        TreeNode node = root;
        while (node != null) {
            if (target == node.val) {
                return node.val;
            }
            result = Math.abs(node.val - target) < Math.abs(result - target) ? node.val : result;
            node = target < node.val ? node.left : node.right;
        }
        return result;
    }
    
    
        // O(n) inOrder
//     public int closestValue(TreeNode root, double target) {
//         if (root == null) {
//             return -1;
//         }
        
//         // ArrayList<Integer> list = new ArrayList();
//         int[] result = {root.val};
//         inOrder(root, result, target);
//         return result[0];
//     }
    
//     private void inOrder(TreeNode root, int[] result, double target) {
//         if (root == null) {
//             return;
//         }
//         inOrder(root.left, result, target);
//         if (Math.abs(result[0] - target) > Math.abs(root.val - target)) {
//             result[0] = root.val;
//         }
//         inOrder(root.right, result, target);
//     }
}
```



## 702 [Search in a Sorted Array of Unknown Size](https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size)    

```java
class Solution {
    public int search(ArrayReader reader, int target) {
        int curr = 0;
        int left = 0, right = 0;
        while (reader.get(curr) < target) {
            left = curr;
            curr = (curr + 1) * 2 - 1;
            right = curr;
        }
        if (reader.get(curr) == target) {
            return curr;
        }
        return binarySearch(reader, left, right, target);
    }
    
    private int binarySearch(ArrayReader reader, int left, int right, int target) {
        while (left <= right) {
            int middle = left + (right - left) / 2;
            if (reader.get(middle) < target) {
                left = middle + 1;
            }
            else if (reader.get(middle) > target) {
                right = middle - 1;
            }
            else {
                return middle;
            }
        }
        return -1;
    }
}
```





## 50 [Pow(x, n)](https://leetcode.com/problems/powx-n)    

```java
class Solution {
    
//     public double myPow(double x, long n) {
//         if (n == 0) {
//             return 1;
//         }
//         if (n < 0) {
     
//             n = -n;
//             x = 1 / x;
//         }

//         return n % 2 == 0 ? myPow(x * x, n / 2) : x * myPow(x * x, n / 2);
//     }
    
    
    public double myPow(double x, int n) {
        if (n == 0) {
            return 1;
        }
        
        if (n == Integer.MIN_VALUE) {
            // if (x > 1) {
            //     return 0.0;
            // }
            // if (x < 1) {
            //     n = Integer.MAX_VALUE;
            //     return x * myPow(x, n);
            // }
            
            n = Integer.MAX_VALUE;
            return 1 / x * myPow(1 / x, n);
        }
        if (n < 0) {
            n = -n;
            x = 1 / x;
        }

        return n % 2 == 0 ? myPow(x * x, n / 2) : x * myPow(x * x, n / 2);
    }
}
```



## 367 [Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square)    

```java
class Solution {
    public boolean isPerfectSquare(int num) {
        int left = 1, right = num;
        while (left <= right) {
            long middle = left + (right - left) / 2;
            // long middle = (left + right) >>> 1;
            long sqr = middle * middle;
            if (sqr < num) {
                left = (int)middle + 1;
            }
            else if (sqr > num) {
                right = (int)middle - 1;
            }
            else {
                return true;
            }
        }
        return false;
    }
    
    
    // public boolean isPerfectSquare(int num) {
    //     int low = 1, high = num;
    //     while (low <= high) {
    //         long mid = (low + high) >>> 1;
    //         if (mid * mid == num) {
    //             return true;
    //         } else if (mid * mid < num) {
    //             low = (int) mid + 1;
    //         } else {
    //             high = (int) mid - 1;
    //         }
    //     }
    //     return false;
    // }
    
    
    // public boolean isPerfectSquare(int num) {
    //     int left = 1; int right = num;
    //     while (left <= right) {
    //         int middle = left + (right - left) / 2;
    //         if (middle < num / middle) {
    //             left = middle + 1;
    //         }
    //         else if (middle > num / middle) {
    //             right = middle - 1;
    //         }
    //         else { 
    //             if (num % middle == 0) {
    //                 return true;
    //             } else {
    //                 left = middle + 1;
    //             }
    //         }
    //     }
    //     return false;
    // }
}
```



## 744 [Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target)    

```java
class Solution {
    // public char nextGreatestLetter(char[] letters, char target) {
    //     if (letters == null || letters.length == 0) {
    //         throw new java.lang.Error("this is very bad");
    //     }
    //     int left = 0, right = letters.length - 1;
    //     while (left + 1 < right) {
    //         int middle = left + (right - left) / 2;
    //         if (letters[middle] < target) {
    //             left = middle;
    //         } 
    //         else if (letters[middle] > target) {
    //             right = middle;
    //         }
    //         else {
    //             left = middle;
    //         }
    //     }
    //     if (letters[left] > target) {
    //         return letters[left];
    //     }
    //     else if (letters[right] > target) {
    //         return letters[right];
    //     }
    //     else {
    //         return letters[0];
    //     }
    // }
    
    // public char nextGreatestLetter(char[] letters, char target) {
    //     // if (letters == null || letters.length == 0) {
    //     //     throw new java.lang.Error("this is very bad");
    //     // }
    //     int left = 0, right = letters.length - 1;
    //     if (letters[right] <= target) {
    //         return letters[0];
    //     }
    //     target++;
    //     while (left < right) {
    //         int middle = left + (right - left) / 2;
    //         if (letters[middle] < target) {
    //             left = middle + 1;
    //         } 
    //         else if (letters[middle] > target) {
    //             right = middle;
    //         }
    //         else {
    //             return letters[middle];
    //         }
    //     }
    //     return letters[left];
    // }
    
        // public char nextGreatestLetter(char[] letters, char target) {
    //     // if (letters == null || letters.length == 0) {
    //     //     throw new java.lang.Error("this is very bad");
    //     // }
    //     int left = 0, right = letters.length - 1;
    //     if (letters[right] <= target) {
    //         return letters[0];
    //     }
    //     while (left < right) {
    //         int middle = left + (right - left) / 2;
    //         if (letters[middle] < target) {
    //             left = middle + 1;
    //         } 
    //         else if (letters[middle] > target) {
    //             right = middle;
    //         }
    //         else {
    //             left = middle + 1;
    //         }
    //     }
    //     return letters[left];
    //     // if (letters[left] > target) {
    //     //     return letters[left];
    //     // }
    //     // else {
    //     //     return letters[0];
    //     // }
    // }
    
    public char nextGreatestLetter(char[] letters, char target) {
        int left = 0, right = letters.length;
        while (left < right) {
            int middle = left + (right - left) / 2;
            if (letters[middle] < target) {
                left = middle + 1;
            } 
            else if (letters[middle] > target) {
                right = middle;
            }
            else {
                left = middle + 1;
            }
        }
        return letters[left % letters.length];
    }
}
```



## 153 [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array)    

```java
class Solution {
    
    // public int findMin(int[] nums) {
    //     if (nums == null || nums.length == 0) {
    //         return -1;
    //     }
    //     int left = 0;
    //     int right = nums.length - 1;
    //     while (left < right) {
    //         if (nums[left] < nums[right]) {
    //             return nums[left];
    //         }
    //         int middle = left + (right - left) / 2;
    //         if (nums[middle] > nums[left]) {
    //             left = middle + 1;
    //         }
    //         else if (nums[middle] == nums[left]) {
    //             left = middle + 1;
    //         }
    //         else {
    //             right = middle;
    //         }
    //     }
    //     return nums[left];
    // }
    
    
//     public int findMin(int[] nums) {
//         if (nums == null || nums.length == 0) {
//             return -1;
//         }
//         int left = 0;
//         int right = nums.length - 1;
 
//         while (left < right) {
//             if (nums[left] < nums[right]) {
//                 return nums[left];
//             }
//             int middle = left + (right - left) / 2;
//             if (nums[middle] > nums[0]) {
//                 left = middle + 1;
//             }
//             else if (nums[middle] == nums[0]) {
//                 left = middle + 1;
//             }
//             else {
//                 right = middle;
//             }
//         }
//         return nums[left];
//     }
    
    public int findMin(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int last = nums[nums.length - 1];
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            if (nums[left] < nums[right]) {
                return nums[left];
            }
            int middle = left + (right - left) / 2;
            if (nums[middle] > last) {
                left = middle + 1;
            }
            else {
                right = middle;
            }
        }
        return nums[left];
    }
    
    // public int findMin(int[] nums) {
    //     if (nums == null || nums.length == 0) {
    //         return -1;
    //     }
    //     int last = nums[nums.length - 1];
    //     int left = 0;
    //     int right = nums.length - 1;
    //     while (left + 1 < right) {
    //         int middle = left + (right - left) / 2;
    //         if (nums[middle] > last) {
    //             left = middle;
    //         }
    //         else {
    //             right = middle;
    //         }
    //     }
    //     return nums[left] < nums[right] ? nums[left] : nums[right];
    // }
}
```





## 154 [Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii)    

```java
class Solution { 
    public int findMin(int[] nums) {
        int left = 0, right = nums.length - 1;
       
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] < nums[right]) {
                right = mid;
            }
            else if (nums[mid] > nums[right]) {
                left = mid + 1;
            }
            else {
                right--;
            }
        }
        return nums[left];
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





## 167 [Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted)  

```java
class Solution {
    // public int[] twoSum(int[] numbers, int target) {
    //     int l = 0;
    //     int r = numbers.length - 1;
    //     while (l < r) {
    //         int sum = numbers[l] + numbers[r];
    //         if (sum < target) {
    //             l++;
    //         }
    //         else if (sum > target) {
    //             r--;
    //         }
    //         else {
    //             int[] result = {l + 1, r + 1};
    //             return result;
    //         }
    //     }
    //     return null;
    // }
    
    public int[] twoSum(int[] numbers, int target) {
        int[] result = new int[2];
        if (numbers == null || numbers.length < 2) {
            return result;
        }
        
        int l = 0;
        int r = numbers.length - 1;
        while (l < r) {
            int sum = numbers[l] + numbers[r];
            if (sum < target) {
                l++;
            }
            else if (sum > target) {
                r--;
            }
            else {
                result[0] = l + 1;
                result[1] = r + 1;
                // break;
                return result;
            }
        }
        return result;
    }
}
```





## 287 [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number)    

```java
class Solution {
//     public int findDuplicate(int[] nums) {
//         // anser is [1, n]
//         int left = 1, right = nums.length - 1;
//         while (left < right) {
//             int mid = left + (right - left) / 2;
//             int num = getLessThanTarget(nums, mid);
//             //抽屉原理Pigeonhole principle：only when num >= mid + 1，answer <= num, when num < mid + 1 or <= mid, then answer > mid
//             if (num < mid) {
//                 left = mid + 1;
//             }
//             else if (num > mid){
//                 right = mid;
//             }
//             else {
//                 left = mid + 1;
//             }
//         }
//         return left;
//     }
    
    
//     private int getLessThanTarget(int[] nums, int thread) {
//         int sum = 0;
//         for (int element : nums) {
//             if (element <= thread) {
//                 sum++;
//             }
//         }
//         return sum;
//     }
    
//     public int findDuplicate(int[] nums) {
//         // anser is [1, n]
//         int left = 1, right = nums.length - 1;
//         while (left + 1 < right) {
//             int mid = left + (right - left) / 2;
//             int num = getLessThanTarget(nums, mid);
//             //抽屉原理Pigeonhole principle：only when num >= mid + 1，answer <= num, when num < mid + 1 or <= mid, then answer > mid
//             if (num < mid) {
//                 left = mid;
//             }
//             else if (num > mid){
//                 right = mid;
//             }
//             else {
//                 left = mid;
//             }
//         }
//         return getLessThanTarget(nums, left) >= left + 1 ? left : right;
//     }
    
    
//     private int getLessThanTarget(int[] nums, int thread) {
//         int sum = 0;
//         for (int element : nums) {
//             if (element <= thread) {
//                 sum++;
//             }
//         }
//         return sum;
//     }
    
    
    // public int findDuplicate(int[] nums) {
    //     // anser is [1, n]
    //     Set<Integer> set = new HashSet();
    //     for (int element : nums) {
    //         if (!set.add(element)) {
    //             return element;
    //         }
    //     }
    //     return -1;
    // }
    
    
    // public int findDuplicate(int[] nums) {
    //     // anser is [1, n]
    //     Set<Integer> set = new HashSet();
    //     for (int element : nums) {
    //         if (!set.add(element)) {
    //             return element;
    //         }
    //     }
    //     return -1;
    // }
    
    public int findDuplicate(int[] nums) {
        // anser is [1, n]
        
        if (nums == null || nums.length < 2) {
            return -1;
        }
        
        int slow = nums[0], fast = nums[0]; //or 0, 0
        
        // boolean isMoved = false;
        //isMoved is guaranteed for at least do once
        // while (isMoved == false || (isMoved = true && slow != fast)) {
        //     if (isMoved == false) {
        //         isMoved = true;
        //     }
        //     slow = nums[slow];
        //     fast = nums[nums[fast]];
        // }
        
        //at least do once
        do {
            slow = nums[slow];
            fast = nums[nums[fast]]; 
        } while (slow != fast);
        
        fast = nums[0]; // or 0 if int slow = 0, fast = 0;
        while (fast != slow) {
            slow = nums[slow];
            fast = nums[fast];
        }
        return slow;
    }
}
```





## 4 [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays)     

```java
// class Solution {
//     public double findMedianSortedArrays(int[] nums1, int[] nums2) {
//         // if (nums1 == null && nums2 == null) {
//         //     throws error
//         // }
        
//         int len1 = nums1.length;
//         int len2 = nums2.length;
//         if (len1 == 0 && len2 == 0) {
//             return 0.0;
//         }
        
//         int[] num = new int[len1 + len2];
//         int pointer1 = 0;
//         int pointer2 = 0;
//         while (pointer1 < len1 && pointer2 < len2) {
//             if (nums1[pointer1] <= nums2[pointer2]) {
//                 num[pointer1 + pointer2] = nums1[pointer1];
//                 pointer1++;
//             }
//             else {
//                 num[pointer1 + pointer2] = nums2[pointer2];
//                 pointer2++;
//             }
//         }
        
//         if (pointer1 == len1) {
//             for (int i = pointer2; i < len2; i++) {
//                 num[len1 + i] = nums2[i];
//             }
//         }
        
//         if (pointer2 == len2) {
//             for (int i = pointer1; i < len1; i++) {
//                 num[len2 + i] = nums1[i];
//             }
//         }
        
//         if ((len1 + len2) % 2 == 0) {
//             return 1.0 * (num[num.length / 2 - 1] + num[num.length / 2]) / 2;
//         }
//         return 1.0 * num[num.length / 2];
//     }
// }



// class Solution {
//     public double findMedianSortedArrays(int[] nums1, int[] nums2) {
//         // if (nums1 == null && nums2 == null) {
//         //     throws error
//         // }
        
//         int len1 = nums1.length;
//         int len2 = nums2.length;
//         if (len1 == 0 && len2 == 0) {
//             return 0.0;
//         }
        
//         int[] num = new int[len1 + len2];
//         int pointer1 = 0;
//         int pointer2 = 0;
        
//         int left = (len1 + len2) / 2, right = (len1 + len2) / 2;
//         int left_value = 0;
//         int right_value = 0;
        
//         if ((len1 + len2) % 2 == 0) {
//             left--;
//         }
//         // System.out.println("left" + left);
//         // System.out.println("right" + right);
//         while (pointer1 < len1 && pointer2 < len2) {
//             if (nums1[pointer1] <= nums2[pointer2]) {
//                 if (pointer1 + pointer2 == left) {
//                     left_value = nums1[pointer1];
//                 }
//                 if (pointer1 + pointer2 == right) {
//                     right_value = nums1[pointer1];
//                     return 1.0 * (left_value + right_value) / 2;
//                 }
//                 pointer1++;
//             }
//             else {
//                 if (pointer1 + pointer2 == left) {
//                     left_value = nums2[pointer2];
//                 }
//                 if (pointer1 + pointer2 == right) {
//                     right_value = nums2[pointer2];
//                     return 1.0 * (left_value + right_value) / 2;
//                 }
//                 pointer2++;
//             }
//         }
        
//         if (pointer1 == len1) {
//             while (pointer2 < len2) {
//                 if (pointer1 + pointer2 == left) {
//                     left_value = nums2[pointer2];
//                 }
//                 if (pointer1 + pointer2 == right) {
//                     right_value = nums2[pointer2];
//                     return 1.0 * (left_value + right_value) / 2;
//                 }
//                 pointer2++;
//             }
//         }
        
//         if (pointer2 == len2) {
//             while (pointer1 < len1) {
//                 if (pointer1 + pointer2 == left) {
//                     left_value = nums1[pointer1];
//                 }
//                 if (pointer1 + pointer2 == right) {
//                     right_value = nums1[pointer1];
//                     return 1.0 * (left_value + right_value) / 2;
//                 }
//                 pointer1++;
//             }
//         }
//         return 0.0;
//     }
// }





// class Solution {
//     public double findMedianSortedArrays(int[] nums1, int[] nums2) {
//         // if (nums1 == null && nums2 == null) {
//         //     throws error
//         // }
        
//         int len1 = nums1.length;
//         int len2 = nums2.length;
//         if (len1 == 0 && len2 == 0) {
//             return 0.0;
//         }
        
//         int[] num = new int[len1 + len2];
//         int pointer1 = 0;
//         int pointer2 = 0;
        
//         int left = (len1 + len2) / 2, right = (len1 + len2) / 2;
//         int left_value = 0;
//         int right_value = 0;
        
//         if ((len1 + len2) % 2 == 0) {
//             left--;
//         }
        
//         while (pointer1 + pointer2 < len1 + len2) {
//             // pointer1 != len1 ==> [] [2] 
//             if (pointer2 == len2 || (pointer1 != len1 && nums1[pointer1] <= nums2[pointer2])) {
//                 if (pointer1 + pointer2 == left) {
//                     left_value = nums1[pointer1];
//                 }
//                 if (pointer1 + pointer2 == right) {
//                     right_value = nums1[pointer1];
//                     return 1.0 * (left_value + right_value) / 2;
//                 }
                
//                 pointer1++;
//             }
//             // pointer1 != len1 ==> [] [2] 
//             if (pointer1 == len1 || (pointer2 != len2 && nums1[pointer1] > nums2[pointer2])) {
//                 if (pointer1 + pointer2 == left) {
//                     left_value = nums2[pointer2];
//                 }
//                 if (pointer1 + pointer2 == right) {
//                     right_value = nums2[pointer2];
//                     return 1.0 * (left_value + right_value) / 2;
//                 }
                
//                 pointer2++;
//             }
//         }
        
//         return 0.0;
//     }
// }








class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        // if (nums1 == null && nums2 == null) {
        //     throws error
        // }
        
        int len1 = nums1.length;
        int len2 = nums2.length;
        if (len1 > len2) {
            return findMedianSortedArrays(nums2, nums1);
        }
        int k = (len1 + len2 + 1) / 2;
        int left = 0;
        int right = len1;
        int m1;
        int m2;
        
        while (left < right) { 
            m1 = left + (right - left) / 2; // left-biased => right = m1 - 1
            m2 = k - m1;
            if (nums1[m1] < nums2[m2 - 1]) {
                left = m1 + 1;
            }
            else if (nums1[m1] > nums2[m2 - 1]) {
                right = m1;
            }
            else {
                left = m1 + 1;
                //right = m1;
            }
        }
        
        m1 = left;
        m2 = k - left;
        // System.out.println("m1" + m1);
        // System.out.println("m2" + m2);
        
        int mid1 = Math.max(m1 == 0 ? Integer.MIN_VALUE : nums1[m1 - 1], m2 == 0 ? Integer.MIN_VALUE : nums2[m2 - 1]);
        if ((len1 + len2) % 2 == 1) {
            return 1.0 * mid1;
        }
        
        int mid2 = Math.min(m1 >= len1 ? Integer.MAX_VALUE : nums1[m1], m2 >= len2 ? Integer.MAX_VALUE : nums2[m2]);
        return 0.5 * (mid1 + mid2);
    }
}
```





719 [Find K-th Smallest Pair Distance](https://leetcode.com/problems/find-k-th-smallest-pair-distance)    



410 [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum)    