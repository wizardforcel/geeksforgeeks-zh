# 将所有小于或等于`k`的元素组合在一起所需的最小交换

> 原文： [https://www.geeksforgeeks.org/minimum-swaps-required-bring-elements-less-equal-k-together/](https://www.geeksforgeeks.org/minimum-swaps-required-bring-elements-less-equal-k-together/)

给定`n`个正整数和数字`k`的数组。 找到将所有小于或等于`k`的数字加在一起所需的**最小**互换数目。

```
Input:  arr[] = {2, 1, 5, 6, 3}, k = 3
Output: 1

Explanation: 
To bring elements 2, 1, 3 together, swap 
element '5' with '3' such that final array
will be-
arr[] = {2, 1, 3, 6, 5}

Input:  arr[] = {2, 7, 9, 5, 8, 7, 4}, k = 5
Output: 2

```



**简单解决方案**首先计算所有小于或等于`k`的元素（例如`good`）。 现在遍历每个子数组并交换其值大于`k`的那些元素。 该方法的时间复杂度为`O(n^2)`。

**简单方法**是使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)和[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)。

1.  查找所有小于或等于`k`的元素的计数。 假设计数是`cnt`。

2.  对长度为`cnt`的窗口使用两个指针技术，每次都跟踪该范围内有多少个元素大于`k`。 假设总数为`bad`。

3.  对每个长度为`cnt`的窗口重复步骤 2，并在其中最少计数为`bad`。 这将是最终答案。

## C++ 

```cpp

// C++ program to find minimum swaps required 
// to club all elements less than or equals 
// to k together 
#include <iostream> 
using namespace std; 

// Utility function to find minimum swaps 
// required to club all elements less than 
// or equals to k together 
int minSwap(int *arr, int n, int k) { 

    // Find count of elements which are 
    // less than equals to k 
    int count = 0; 
    for (int i = 0; i < n; ++i) 
        if (arr[i] <= k) 
            ++count; 

    // Find unwanted elements in current 
    // window of size 'count' 
    int bad = 0; 
    for (int i = 0; i < count; ++i) 
        if (arr[i] > k) 
            ++bad; 

    // Initialize answer with 'bad' value of 
    // current window 
    int ans = bad; 
    for (int i = 0, j = count; j < n; ++i, ++j) { 

        // Decrement count of previous window 
        if (arr[i] > k) 
            --bad; 

        // Increment count of current window 
        if (arr[j] > k) 
            ++bad; 

        // Update ans if count of 'bad' 
        // is less in current window 
        ans = min(ans, bad); 
    } 
    return ans; 
} 

// Driver code 
int main() { 

    int arr[] = {2, 1, 5, 6, 3}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int k = 3; 
    cout << minSwap(arr, n, k) << "\n"; 

    int arr1[] = {2, 7, 9, 5, 8, 7, 4}; 
    n = sizeof(arr1) / sizeof(arr1[0]); 
    k = 5; 
    cout << minSwap(arr1, n, k); 
    return 0; 
} 

```

## Java

```java

// Java program to find minimum  
// swaps required to club all 
// elements less than or equals 
// to k together 
import java.lang.*; 

class GFG { 

// Utility function to find minimum swaps 
// required to club all elements less than 
// or equals to k together 
static int minSwap(int arr[], int n, int k) { 

    // Find count of elements which are 
    // less than equals to k 
    int count = 0; 
    for (int i = 0; i < n; ++i) 
    if (arr[i] <= k) 
        ++count; 

    // Find unwanted elements in current 
    // window of size 'count' 
    int bad = 0; 
    for (int i = 0; i < count; ++i) 
    if (arr[i] > k) 
        ++bad; 

    // Initialize answer with 'bad' value of 
    // current window 
    int ans = bad; 
    for (int i = 0, j = count; j < n; ++i, ++j) { 

    // Decrement count of previous window 
    if (arr[i] > k) 
        --bad; 

    // Increment count of current window 
    if (arr[j] > k) 
        ++bad; 

    // Update ans if count of 'bad' 
    // is less in current window 
    ans = Math.min(ans, bad); 
    } 
    return ans; 
} 

// Driver code 
public static void main(String[] args)  
{ 
    int arr[] = {2, 1, 5, 6, 3}; 
    int n = arr.length; 
    int k = 3; 
    System.out.print(minSwap(arr, n, k) + "\n"); 

    int arr1[] = {2, 7, 9, 5, 8, 7, 4}; 
    n = arr1.length; 
    k = 5; 
    System.out.print(minSwap(arr1, n, k)); 
} 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python3 program to find  
# minimum swaps required 
# to club all elements less 
# than or equals to k together 

# Utility function to find  
# minimum swaps required to  
# club all elements less than 
# or equals to k together 
def minSwap(arr, n, k) : 

    # Find count of elements 
    # which are less than  
    # equals to k 
    count = 0
    for i in range(0, n) : 
        if (arr[i] <= k) : 
            count = count + 1

    # Find unwanted elements  
    # in current window of  
    # size 'count' 
    bad = 0
    for i in range(0, count) : 
        if (arr[i] > k) : 
            bad = bad + 1

    # Initialize answer with  
    # 'bad' value of current 
    # window 
    ans = bad 
    j = count 
    for i in range(0, n) : 

        if(j == n) : 
            break

        # Decrement count of 
        # previous window 
        if (arr[i] > k) : 
            bad = bad - 1

        # Increment count of  
        # current window 
        if (arr[j] > k) : 
            bad = bad + 1

        # Update ans if count  
        # of 'bad' is less in 
        # current window 
        ans = min(ans, bad) 

        j = j + 1

    return ans 

# Driver code 
arr = [2, 1, 5, 6, 3] 
n = len(arr) 
k = 3
print (minSwap(arr, n, k)) 

arr1 = [2, 7, 9, 5, 8, 7, 4] 
n = len(arr1) 
k = 5
print (minSwap(arr1, n, k)) 

# This code is contributed by  
# Manish Shaw(manishshaw1) 

```

## C# 

```cs

// C# program to find minimum  
// swaps required to club all 
// elements less than or equals 
// to k together 
using System; 

class GFG { 

    // Utility function to find minimum swaps 
    // required to club all elements less than 
    // or equals to k together 
    static int minSwap(int []arr, int n, int k) { 

        // Find count of elements which are 
        // less than equals to k 
        int count = 0; 
        for (int i = 0; i < n; ++i) 
        if (arr[i] <= k) 
            ++count; 

        // Find unwanted elements in current 
        // window of size 'count' 
        int bad = 0; 
        for (int i = 0; i < count; ++i) 
        if (arr[i] > k) 
            ++bad; 

        // Initialize answer with 'bad' value of 
        // current window 
        int ans = bad; 
        for (int i = 0, j = count; j < n; ++i, ++j) { 

            // Decrement count of previous window 
            if (arr[i] > k) 
                --bad; 

            // Increment count of current window 
            if (arr[j] > k) 
                ++bad; 

            // Update ans if count of 'bad' 
            // is less in current window 
            ans = Math.Min(ans, bad); 
        } 
        return ans; 
    } 

    // Driver code 
    public static void Main()  
    { 
        int []arr = {2, 1, 5, 6, 3}; 
        int n = arr.Length; 
        int k = 3; 
        Console.WriteLine(minSwap(arr, n, k)); 

        int []arr1 = {2, 7, 9, 5, 8, 7, 4}; 
        n = arr1.Length; 
        k = 5; 
        Console.WriteLine(minSwap(arr1, n, k)); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program to find 
// minimum swaps required 
// to club all elements  
// less than or equals 
// to k together 

// Utility function to  
// find minimum swaps 
// required to club all  
// elements less than 
// or equals to k together 
function minSwap($arr, $n, $k) 
{ 

    // Find count of elements 
    // which are less than 
    // equals to k 
    $count = 0; 
    for ($i = 0; $i < $n; ++$i) 
        if ($arr[$i] <= $k) 
            ++$count; 

    // Find unwanted elements in current 
    // window of size 'count' 
    $bad = 0; 
    for ($i = 0; $i < $count; ++$i) 
        if ($arr[$i] > $k) 
            ++$bad; 

    // Initialize answer  
    // with 'bad' value of 
    // current window 
    $ans = $bad; 
    for ($i = 0, $j = $count; $j < $n;  
                           ++$i, ++$j)  
    { 

        // Decrement count of  
        // previous window 
        if ($arr[$i] > $k) 
            --$bad; 

        // Increment count of 
        // current window 
        if ($arr[$j] > $k) 
            ++$bad; 

        // Update ans if count of 'bad' 
        // is less in current window 
        $ans = min($ans, $bad); 
    } 
    return $ans; 
} 

// Driver code 
$arr = array(2, 1, 5, 6, 3); 
$n = sizeof($arr); 
$k = 3; 
echo(minSwap($arr, $n, $k) . "\n"); 

$arr1 = array(2, 7, 9, 5, 8, 7, 4); 
$n = sizeof($arr1); 
$k = 5; 
echo(minSwap($arr1, $n, $k)); 

// This code is contributed by Ajit. 
?> 

```

**输出**：

```
1
2
```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(1)`。



* * *

* * *



