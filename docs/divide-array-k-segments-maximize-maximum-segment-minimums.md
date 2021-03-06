# 将数组划分为`k`个片段，来最大化片段最小值的最大值

> 原文： [https://www.geeksforgeeks.org/divide-array-k-segments-maximize-maximum-segment-minimums/](https://www.geeksforgeeks.org/divide-array-k-segments-maximize-maximum-segment-minimums/)

给定一个由`n`个整数组成的数组，请将其划分为`k`个分段，并找到`k`个分段的最小值中的最大值。 输出在分割`k`个子数组的所有方式中可以获得的最大整数。

**示例**：

```
Input : arr[] = {1, 2, 3, 6, 5}  
        k = 2
Output: 5
Explanation: There are many ways to create 
two segments. The optimal segments are (1, 2, 3)
and (6, 5). Minimum of both segments are 1 and 5, 
hence the maximum(1, 5) is 5\. 

Input: -4 -5 -3 -2 -1 k=1
Output: -5 
Explanation: only one segment, so minimum is -5.

```



将有 3 种情况需要考虑。

1.  **`k >= 3`**：当`k`大于 2 时，一个段将仅由最大元素组成，因此最小段的最大值将始终为`max`。

2.  **`k = 2`**：对于`k = 2`，答案是第一个元素和最后一个元素的最大值。

3.  **`k = 1`**：只有可能的分区是等于整个数组的一个分段。 因此，答案是整个数组上的最小值。

下面是上述方法的实现：

## C++ 

```cpp

// CPP Program to find maximum value of 
// maximum of minimums of k segments. 
#include <bits/stdc++.h> 
using namespace std; 

// function to calculate the max of all the 
// minimum segments 
int maxOfSegmentMins(int a[], int n, int k) 
{ 
    // if we have to divide it into 1 segment 
    // then the min will be the answer 
    if (k == 1)  
       return *min_element(a, a+n); 

    if (k == 2)  
       return max(a[0], a[n-1]);   

    // If k >= 3, return maximum of all 
    // elements. 
    return *max_element(a, a+n); 
} 

// driver program to test the above function 
int main() 
{ 
    int a[] = { -10, -9, -8, 2, 7, -6, -5 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    int k = 2; 
    cout << maxOfSegmentMins(a, n, k); 
} 

```

## Java

```java

// Java Program to find maximum  
// value of maximum of minimums 
// of k segments. 
import java .io.*; 
import java .util.*; 

class GFG 
{ 

    // function to calculate  
    // the max of all the  
    // minimum segments 
    static int maxOfSegmentMins(int []a, 
                                int n,  
                                int k) 
    { 

        // if we have to divide  
        // it into 1 segment then  
        // the min will be the answer 
        if (k == 1)  
        { 
            Arrays.sort(a); 
                return a[0]; 
        } 

        if (k == 2)  
            return Math.max(a[0],  
                            a[n - 1]);  

        // If k >= 3, return  
        // maximum of all  
        // elements. 
        return a[n - 1]; 
    } 

    // Driver Code 
    static public void main (String[] args) 
    { 
        int []a = {-10, -9, -8,  
                    2, 7, -6, -5}; 
        int n = a.length; 
        int k = 2; 

        System.out.println( 
                maxOfSegmentMins(a, n, k)); 
    } 
} 

// This code is contributed 
// by anuj_67\. 

```

## Python3

```py

# Python3 Program to find maximum value of  
# maximum of minimums of k segments. 

# function to calculate the max of all the  
# minimum segments  
def maxOfSegmentMins(a,n,k): 

    # if we have to divide it into 1 segment  
    # then the min will be the answer  
    if k ==1: 
        return min(a) 
    if k==2: 
        return max(a[0],a[n-1]) 

    # If k >= 3, return maximum of all  
    #  elements.  
    return max(a) 

# Driver code 
if __name__=='__main__': 
    a = [-10, -9, -8, 2, 7, -6, -5] 
    n = len(a) 
    k =2
    print(maxOfSegmentMins(a,n,k)) 

# This code is contributed by  
# Shrikant13 

```

## C# 

```cs

// C# Program to find maximum value of 
// maximum of minimums of k segments. 
using System; 
using System.Linq; 

public class GFG { 

    // function to calculate the max 
    // of all the minimum segments 
    static int maxOfSegmentMins(int []a, 
                             int n, int k) 
    { 

        // if we have to divide it into 1 
        // segment then the min will be 
        // the answer 
        if (k == 1)  
            return a.Min(); 

        if (k == 2)  
            return Math.Max(a[0], a[n - 1]);  

        // If k >= 3, return maximum of 
        // all elements. 
        return a.Max(); 
    } 

    // Driver function 
    static public void Main () 
    { 
        int []a = { -10, -9, -8, 2, 7, 
                                 -6, -5 }; 
        int n = a.Length; 
        int k = 2; 

        Console.WriteLine( 
                  maxOfSegmentMins(a, n, k)); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP Program to find maximum 
// value of maximum of minimums 
// of k segments. 

// function to calculate 
// the max of all the 
// minimum segments 
function maxOfSegmentMins($a, $n, $k) 
{ 
    // if we have to divide  
    // it into 1 segment then 
    // the min will be the answer 
    if ($k == 1)  
    return min($a); 

    if ($k == 2)  
    return max($a[0],  
               $a[$n - 1]);  

    // If k >= 3, return  
    // maximum of all elements. 
    return max($a); 
} 

// Driver Code 
$a = array(-10, -9, -8,  
            2, 7, -6, -5); 
$n = count($a); 
$k = 2; 
echo maxOfSegmentMins($a, $n, $k); 

// This code is contributed by vits. 
?> 

```

**输出**：

```
-5
```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(1)`。



