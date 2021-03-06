# 排除某些元素的最大子数组总和

> 原文： [https://www.geeksforgeeks.org/maximum-subarray-sum-excluding-certain-elements/](https://www.geeksforgeeks.org/maximum-subarray-sum-excluding-certain-elements/)

给定`n`个整数的`A`数组和`m`个整数的`B`数组，找到数组`A`的最大连续子数组总和，以使该子数组中不存在数组`B`的任何元素。

**示例**：

> 输入：`A = {1, 7, -10, 6, 2}`, `B = {5, 6, 7, 1}`
> 
> 输出：2
> 
> 说明： 
> 
> `A`的任何元素不允许在数组`B`中存在。
> 
> 满足此条件的最大和子数组为`{2}`，因为唯一允许的子数组为：`{-10}`和`{2}`。 最大和子数组为`{2}`，总计为 2
> 
> 输入：`A = {3, 4, 5, -4, 6}`, `B = {1, 8, 5}`
> 
> 输出：7
> 
> 说明：
> 
> 满足此要求的最大和子数组为`{3, 4}`，因为唯一允许的子数组为`{3}`，`{4}`，`{3, 4}`，`{-4}`，`{6}`，`{-4, 6}`。 最大和子数组为`{3, 4}`，总计为 7

**方法 1（`O(n * m)`方法）**：

我们可以使用 [Kadane 算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)解决此问题。 由于我们不希望数组`B`的任何元素成为`A`的任何子数组的一部分，因此我们需要对经典的 Kadane 算法进行一些修改。

每当我们考虑 Kadane 算法中的元素时，我们要么扩展当前子数组，要么开始一个新的子数组。

```
curr_max = max(a[i], curr_max+a[i]);
if (curr_max < 0)
   curr_max = 0

```

现在，在这个问题中，当我们考虑任何元素时，我们通过在数组`B`中[线性搜索](https://www.geeksforgeeks.org/linear-search/)进行检查，如果该元素存在于`B`中，则将`curr_max`设置为零，这意味着在该索引处我们考虑的所有子数组将结束，并且不会进一步扩展，因为无法形成其他连续数组。

如果`B`中存在`A[i]`，则无法进一步扩展`A`中从 0 到`i - 1`的所有子数组，因为第`i`元素永远不会包含在任何子数组中。

如果数组`A`的当前元素不是数组`B`的一部分，我们将继续使用 Kadane 算法，并跟踪`max_so_far`。

## C++ 

```cpp

// C++ Program to find max subarray 
// sum excluding some elements 
#include <bits/stdc++.h> 
using namespace std; 

// Function to check the element  
// present in array B 
bool isPresent(int B[], int m, int x) 
{ 
    for (int i = 0; i < m; i++) 
        if (B[i] == x) 
            return true; 
    return false; 
} 

// Utility function for findMaxSubarraySum() 
// with the following parameters  
// A => Array A, 
// B => Array B, 
// n => Number of elements in Array A, 
// m => Number of elements in Array B  
int findMaxSubarraySumUtil(int A[], int B[], 
                        int n, int m) 
{ 

    // set max_so_far to INT_MIN 
    int max_so_far = INT_MIN, curr_max = 0; 

    for (int i = 0; i < n; i++) { 

        // if the element is present in B,  
        // set current max to 0 and move to  
        // the next element */ 
        if (isPresent(B, m, A[i])) { 
            curr_max = 0; 
            continue; 
        } 

        // Proceed as in Kadane's Algorithm  
        curr_max = max(A[i], curr_max + A[i]); 
        max_so_far = max(max_so_far, curr_max); 
    } 
    return max_so_far; 
} 

// Wrapper for findMaxSubarraySumUtil()  
void findMaxSubarraySum(int A[], int B[], 
                        int n, int m) 
{ 
    int maxSubarraySum = findMaxSubarraySumUtil(A, B, 
                                                n, m); 

    // This case will occour when all elements 
    // of A are present in B, thus 
    // no subarray can be formed  
    if (maxSubarraySum == INT_MIN) { 
        cout << "Maximum Subarray Sum cant be found"
             << endl; 
    } 
    else { 
        cout << "The Maximum Subarray Sum = "
            << maxSubarraySum << endl; 
    } 
} 

// Driver Code 
int main() 
{ 
    int A[] = { 3, 4, 5, -4, 6 }; 
    int B[] = { 1, 8, 5 }; 

    int n = sizeof(A) / sizeof(A[0]); 
    int m = sizeof(B) / sizeof(B[0]); 

    // Calling function 
    findMaxSubarraySum(A, B, n, m); 

    return 0; 
} 

```

## Java

```java

// Java Program to find max subarray 
// sum excluding some elements 
import java.io.*; 

class GFG { 

    // Function to check the element  
    // present in array B 
    static boolean isPresent(int B[], 
                            int m, 
                            int x) 
    { 
        for (int i = 0; i < m; i++) 
            if (B[i] == x) 
                return true; 

        return false; 
    } 

    // Utility function for findMaxSubarraySum() 
    // with the following parameters 
    // A => Array A, 
    // B => Array B, 
    // n => Number of elements in Array A, 
    // m => Number of elements in Array B 
    static int findMaxSubarraySumUtil(int A[], int B[], 
                                      int n, int m) 
    { 

        // set max_so_far to INT_MIN 
        int max_so_far = -2147483648, curr_max = 0; 

        for (int i = 0; i < n; i++) { 

            // if the element is present in B, 
            // set current max to 0 and move to 
            // the next element 
            if (isPresent(B, m, A[i])) { 
                curr_max = 0; 
                continue; 
            } 

            // Proceed as in Kadane's Algorithm 
            curr_max = Math.max(A[i], curr_max + A[i]); 
            max_so_far = Math.max(max_so_far, curr_max); 
        } 
        return max_so_far; 
    } 

    // Wrapper for findMaxSubarraySumUtil() 
    static void findMaxSubarraySum(int A[], int B[], 
                                   int n, int m) 
    { 
        int maxSubarraySum = findMaxSubarraySumUtil(A, B, 
                                                    n, m); 

        // This case will occour when all 
        // elements of A are present 
        // in B, thus no subarray can be formed 
        if (maxSubarraySum == -2147483648) { 
                        System.out.println("Maximum Subarray Sum"
                                        + " " + "can't be found"); 

        } 
        else { 
            System.out.println("The Maximum Subarray Sum = "
                                + maxSubarraySum); 
        } 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 

        int A[] = { 3, 4, 5, -4, 6 }; 
        int B[] = { 1, 8, 5 }; 

        int n = A.length; 
        int m = B.length; 

        // Calling Function 
        findMaxSubarraySum(A, B, n, m); 
    } 
} 

// This code is contributed by Ajit. 

```

## Python3

```py

# Python Program to find max  
# subarray sum excluding some 
# elements  

# Function to check the element  
# present in array B  
INT_MIN = -2147483648

def isPresent(B, m, x): 
    for i in range(0, m): 
        if B[i] == x: 
            return True
    return False

# Utility function for findMaxSubarraySum()  
# with the following parameters  
# A => Array A,  
# B => Array B,  
# n => Number of elements in Array A,  
# m => Number of elements in Array B  
def findMaxSubarraySumUtil(A, B, n, m):  

    #set max_so_far to INT_MIN 
    max_so_far = INT_MIN 
    curr_max = 0
    for i in range(0, n): 
        if isPresent(B, m, A[i]) == True: 
            curr_max = 0
            continue

        # Proceed as in Kadane's Algorithm 
        curr_max = max(A[i], curr_max + A[i]) 
        max_so_far = max(max_so_far, curr_max) 
    return max_so_far 

# Wrapper for findMaxSubarraySumUtil() 
def findMaxSubarraySum(A, B, n, m): 

    maxSubarraySum = findMaxSubarraySumUtil(A, B, n, m) 

    # This case will occour when all   
    # elements of A are present  
    # in B, thus no subarray can be  
    # formed  
    if maxSubarraySum == INT_MIN: 
        print('Maximum Subarray Sum cant be found') 
    else: 
        print('The Maximum Subarray Sum =',  
                            maxSubarraySum) 

# Driver code 
A = [3, 4, 5, -4, 6 ] 
B = [ 1, 8, 5 ] 
n = len(A) 
m = len(B) 

# Calling function  
findMaxSubarraySum(A, B, n, m) 

# This code is contributed 
# by sahil shelangia 

```

## C# 

```cs

// C# Program to find max subarray 
// sum excluding some elements 
using System; 

class GFG { 

    // Function to check the element  
    // present in array B 
    static bool isPresent(int[] B, int m,  
                                   int x) 
    { 
        for (int i = 0; i < m; i++) 
            if (B[i] == x) 
                return true; 

        return false; 
    } 

    // Utility function for findMaxSubarraySum() 
    // with the following parameters 
    // A => Array A, 
    // B => Array B, 
    // n => Number of elements in Array A, 
    // m => Number of elements in Array B 
    static int findMaxSubarraySumUtil(int[] A, int[] B, 
                                      int n, int m) 
    { 

        // set max_so_far to INT_MIN 
        int max_so_far = -2147483648, curr_max = 0; 

        for (int i = 0; i < n; i++) { 

            // if the element is present in B, 
            // set current max to 0 and move to 
            // the next element 
            if (isPresent(B, m, A[i])) { 
                curr_max = 0; 
                continue; 
            } 

            // Proceed as in Kadane's Algorithm 
            curr_max = Math.Max(A[i], curr_max + A[i]); 
            max_so_far = Math.Max(max_so_far, curr_max); 
        } 
        return max_so_far; 
    } 

    // Wrapper for findMaxSubarraySumUtil() 
    static void findMaxSubarraySum(int[] A, int[] B, 
                                    int n, int m) 
    { 
        int maxSubarraySum = findMaxSubarraySumUtil(A, B, 
                                                    n, m); 

        // This case will occour when all 
        // elements of A are present 
        // in B, thus no subarray can be formed 
        if (maxSubarraySum == -2147483648) 
        { 
            Console.Write("Maximum Subarray Sum"
                           + " " + "can't be found"); 

        } 
        else 
        { 
            Console.Write("The Maximum Subarray Sum = "
                           + maxSubarraySum); 
        } 
    } 

    // Driver Code 
    static public void Main () 
    { 

        int[] A = {3, 4, 5, -4, 6}; 
        int[] B = {1, 8, 5}; 

        int n = A.Length; 
        int m = B.Length; 

        // Calling Function 
        findMaxSubarraySum(A, B, n, m); 

    } 
} 

// This code is contributed by Shrikant13\. 

```

## PHP

```php

<?php 
// PHP Program to find max subarray 
// sum excluding some elements 

// Function to check the element  
// present in array B 
function isPresent($B, $m, $x) 
{ 
    for ($i = 0; $i < $m; $i++) 
        if ($B[$i] == $x) 
            return true; 
    return false; 
} 

// Utility function for  
// findMaxSubarraySum()  
// with the following  
// parameters  
// A => Array A, 
// B => Array B, 
// n => Number of elements 
//      in Array A, 
// m => Number of elements  
//      in Array B  
function findMaxSubarraySumUtil($A, $B, 
                                $n, $m) 
{ 

    // set max_so_far 
    // to INT_MIN 
    $max_so_far = PHP_INT_MIN; 
    $curr_max = 0; 

    for ($i = 0; $i < $n; $i++)  
    { 

        // if the element is present  
        // in B, set current max to  
        // 0 and move to the next  
        // element  
        if (isPresent($B, $m, $A[$i])) 
        { 
            $curr_max = 0; 
            continue; 
        } 

        // Proceed as in 
        // Kadane's Algorithm  
        $curr_max = max($A[$i],  
        $curr_max + $A[$i]); 
        $max_so_far = max($max_so_far,  
                          $curr_max); 
    } 
    return $max_so_far; 
} 

// Wrapper for  
// findMaxSubarraySumUtil()  
function findMaxSubarraySum($A, $B, 
                            $n, $m) 
{ 
    $maxSubarraySum = findMaxSubarraySumUtil($A, $B, 
                                             $n, $m); 

    // This case will occour  
    // when all elements of  
    // A are present in 
    // B, thus no subarray  
    // can be formed  
    if ($maxSubarraySum == PHP_INT_MIN)  
    { 
        echo ("Maximum Subarray " .  
            "Sum cant be found\n"); 
    } 
    else 
    { 
        echo ("The Maximum Subarray Sum = ".  
                     $maxSubarraySum. "\n"); 
    } 
} 

// Driver Code 
$A = array(3, 4, 5, -4, 6); 
$B = array(1, 8, 5); 

$n = count($A); 
$m = count($B); 

// Calling function 
findMaxSubarraySum($A, $B, $n, $m); 

// This code is contributed by  
// Manish Shaw(manishshaw1) 
?> 

```

**输出**：

```
The Maximum Subarray Sum = 7

```

这种方法的时间复杂度为`O(n * m)`。

**方法 2（`O((n + m) * log(m))`方法）**：

该方法背后的主要思想与方法 1 完全相同。 使用[**二分搜索**](http://www.geeksforgeeks.org/binary-search/)，可以更快地使用数组`B`中的数组`A`的元素。

## C++

```cpp

// C++ Program to find max subarray  
// sum excluding some elements 
#include <bits/stdc++.h> 
using namespace std; 

// Utility function for findMaxSubarraySum() 
// with the following parameters  
// A => Array A, 
// B => Array B, 
// n => Number of elements in Array A, 
// m => Number of elements in Array B  
int findMaxSubarraySumUtil(int A[], int B[], 
                           int n, int m) 
{ 

    // set max_so_far to INT_MIN 
    int max_so_far = INT_MIN, curr_max = 0; 

    for (int i = 0; i < n; i++) { 

        // if the element is present in B,  
        // set current max to 0 and move to 
        // the next element  
        if (binary_search(B, B + m, A[i])) { 
            curr_max = 0; 
            continue; 
        } 

        // Proceed as in Kadane's Algorithm  
        curr_max = max(A[i], curr_max + A[i]); 
        max_so_far = max(max_so_far, curr_max); 
    } 
    return max_so_far; 
} 

// Wrapper for findMaxSubarraySumUtil() 
void findMaxSubarraySum(int A[], int B[],  
                        int n, int m) 
{ 
    // sort array B to apply Binary Search 
    sort(B, B + m); 

    int maxSubarraySum = findMaxSubarraySumUtil(A, B,  
                                                n, m); 

    // This case will occour when all elements 
    // of A are present in B, thus no subarray  
    // can be formed  
    if (maxSubarraySum == INT_MIN) { 
        cout << "Maximum subarray sum cant be found"
            << endl; 
    } 
    else { 
        cout << "The Maximum subarray sum = "
             << maxSubarraySum << endl; 
    } 
} 

// Driver Code 
int main() 
{ 
    int A[] = { 3, 4, 5, -4, 6 }; 
    int B[] = { 1, 8, 5 }; 

    int n = sizeof(A) / sizeof(A[0]); 
    int m = sizeof(B) / sizeof(B[0]); 

    // Calling fucntion 
    findMaxSubarraySum(A, B, n, m); 
    return 0; 
} 

```

## Java

```java

// Java Program to find max subarray  
// sum excluding some elements 
import java.util.*; 

class GFG  
{ 

    // Utility function for findMaxSubarraySum() 
    // with the following parameters  
    // A => Array A, 
    // B => Array B, 
    // n => Number of elements in Array A, 
    // m => Number of elements in Array B  
    static int findMaxSubarraySumUtil(int A[], int B[], 
                                        int n, int m)  
    { 

        // set max_so_far to INT_MIN 
        int max_so_far = Integer.MIN_VALUE, curr_max = 0; 

        for (int i = 0; i < n; i++)  
        { 

            // if the element is present in B,  
            // set current max to 0 and move to 
            // the next element  
            if (Arrays.binarySearch(B, A[i]) >= 0)  
            { 
                curr_max = 0; 
                continue; 
            } 

            // Proceed as in Kadane's Algorithm  
            curr_max = Math.max(A[i], curr_max + A[i]); 
            max_so_far = Math.max(max_so_far, curr_max); 
        } 
        return max_so_far; 
    } 

    // Wrapper for findMaxSubarraySumUtil() 
    static void findMaxSubarraySum(int A[], int B[], 
                                        int n, int m)  
    { 
        // sort array B to apply Binary Search 
        Arrays.sort(B); 

        int maxSubarraySum = findMaxSubarraySumUtil(A, B, 
                n, m); 

        // This case will occour when all elements 
        // of A are present in B, thus no subarray  
        // can be formed  
        if (maxSubarraySum == Integer.MIN_VALUE)  
        { 
            System.out.println("Maximum subarray sum cant be found"); 
        }  
        else 
        { 
            System.out.println("The Maximum subarray sum = "
                    + maxSubarraySum); 
        } 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        int A[] = {3, 4, 5, -4, 6}; 
        int B[] = {1, 8, 5}; 

        int n = A.length; 
        int m = B.length; 

        // Calling fucntion 
        findMaxSubarraySum(A, B, n, m); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
The Maximum subarray sum = 7

```

此方法的时间复杂度为`O(nlog(m) + mlog(m))`或`O((n + m) log(m))`。

注意：`mlog(m)`因子归因于对数组`B`的排序。



* * *

* * *



