# 查询二进制数组的子数组的十进制值

> 原文： [https://www.geeksforgeeks.org/queries-for-decimal-values-of-subarray-of-a-binary-array/](https://www.geeksforgeeks.org/queries-for-decimal-values-of-subarray-of-a-binary-array/)

给定一个二进制数组`arr[]`，我们找到由子数组`a[l..r]`表示的数字。 有多个此类查询。

**示例**：

```
Input :  arr[] = {1, 0, 1, 0, 1, 1};
         l = 2, r = 4
         l = 4, r = 5
Output : 5
         3 
Subarray 2 to 4 is 101 which is 5 in decimal.
Subarray 4 to 5 is 11 which is 3 in decimal.

Input : arr[] = {1, 1, 1}
        l = 0, r = 2
        l = 1, r = 2
Output : 7
         3

```



**简单解决方案**使用简单的二进制到十进制转换为每个给定范围计算十进制值。 这里每个查询花费`O(len)`时间，其中`len`是范围的长度。

**高效解决方案**将进行每次计算，以便可以在`O(1)`时间内回答查询。

子数组`arr[l..r]`表示的数字是`arr[l] * 2^(r-l) + arr[l + 1] * 2^(r - l - 1) + … + arr[r] * 2^(r-r)`。

1.  使数组`pre[]`的大小与给定数组的大小相同，其中`pre[i]`存储`arr[j] * 2^(n - 1 - j)`的和，其中`j`包括从`i`到`n-1`的每个值。

2.  子数组`arr[l..r]`表示的数字将等于`(pre[l] – pre[r + 1]) / 2^(n-1-r)`，`pre[l] – pre[r + 1]`等于`arr[l] * 2^(n - 1 - l) + arr[l + 1] * 2^(n - 1 - l - 1) + …… + arr[r] * 2^(n - 1 - r)`。 因此，如果我们将其除以`2^(n - 1 - r)`，则会得到所需的答案。

## C++ 

```cpp

// C++ implementation of finding number 
// represented by binary subarray 
#include <bits/stdc++.h> 
using namespace std; 

// Fills pre[] 
void precompute(int arr[], int n, int pre[]) 
{ 
    memset(pre, 0, n * sizeof(int)); 
    pre[n - 1] = arr[n - 1] * pow(2, 0); 
    for (int i = n - 2; i >= 0; i--) 
        pre[i] = pre[i + 1] + arr[i] * (1 << (n - 1 - i)); 
} 

// returns the number represented by a binary 
// subarray l to r 
int decimalOfSubarr(int arr[], int l, int r, 
                    int n, int pre[]) 
{ 
    // if r is equal to n-1 r+1 does not exist 
    if (r != n - 1) 
        return (pre[l] - pre[r + 1]) / (1 << (n - 1 - r)); 

    return pre[l] / (1 << (n - 1 - r)); 
} 

// Driver Function 
int main() 
{ 
    int arr[] = { 1, 0, 1, 0, 1, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    int pre[n]; 
    precompute(arr, n, pre); 
    cout << decimalOfSubarr(arr, 2, 4, n, pre) << endl; 
    cout << decimalOfSubarr(arr, 4, 5, n, pre) << endl; 
    return 0; 
} 

```

## Java

```java

// Java implementation of finding number 
// represented by binary subarray 
import java.util.Arrays; 

class GFG { 

    // Fills pre[] 
    static void precompute(int arr[], int n, int pre[]) 
    { 
        Arrays.fill(pre, 0); 

        pre[n - 1] = arr[n - 1] * (int)(Math.pow(2, 0)); 
        for (int i = n - 2; i >= 0; i--) 
            pre[i] = pre[i + 1] + arr[i] * (1 << (n - 1 - i)); 
    } 

    // returns the number represented by a binary 
    // subarray l to r 
    static int decimalOfSubarr(int arr[], int l, int r, 
                               int n, int pre[]) 
    { 

        // if r is equal to n-1 r+1 does not exist 
        if (r != n - 1) 
            return (pre[l] - pre[r + 1]) / (1 << (n - 1 - r)); 

        return pre[l] / (1 << (n - 1 - r)); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 1, 0, 1, 0, 1, 1 }; 
        int n = arr.length; 

        int pre[] = new int[n]; 
        precompute(arr, n, pre); 

        System.out.println(decimalOfSubarr(arr, 
                                           2, 4, n, pre)); 

        System.out.println(decimalOfSubarr(arr, 
                                           4, 5, n, pre)); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# implementation of finding number 
# represented by binary subarray 
from math import pow

# Fills pre[] 
def precompute(arr, n, pre): 

    pre[n - 1] = arr[n - 1] * pow(2, 0) 
    i = n - 2
    while(i >= 0): 
        pre[i] = (pre[i + 1] + arr[i] * 
                 (1 << (n - 1 - i))) 
        i -= 1

# returns the number represented by  
# a binary subarray l to r 
def decimalOfSubarr(arr, l, r, n, pre): 

    # if r is equal to n-1 r+1 does not exist 
    if (r != n - 1): 
        return ((pre[l] - pre[r + 1]) /
                (1 << (n - 1 - r))) 

    return pre[l] / (1 << (n - 1 - r)) 

# Driver Code 
if __name__ == '__main__': 
    arr = [1, 0, 1, 0, 1, 1] 
    n = len(arr) 

    pre = [0 for i in range(n)] 
    precompute(arr, n, pre) 
    print(int(decimalOfSubarr(arr, 2, 4, n, pre))) 
    print(int(decimalOfSubarr(arr, 4, 5, n, pre))) 

# This code is contributed by 
# Surendra_Gangwar 

```

## C# 

```cs

// C# implementation of finding number 
// represented by binary subarray 
using System; 

class GFG { 

    // Fills pre[] 
    static void precompute(int[] arr, int n, int[] pre) 
    { 
        for (int i = 0; i < n; i++) 
            pre[i] = 0; 

        pre[n - 1] = arr[n - 1] * (int)(Math.Pow(2, 0)); 
        for (int i = n - 2; i >= 0; i--) 
            pre[i] = pre[i + 1] + arr[i] * (1 << (n - 1 - i)); 
    } 

    // returns the number represented by  
    // a binary subarray l to r 
    static int decimalOfSubarr(int[] arr, int l, int r, 
                                      int n, int[] pre) 
    { 
        // if r is equal to n-1 r+1 does not exist 
        if (r != n - 1) 
            return (pre[l] - pre[r + 1]) / (1 << (n - 1 - r)); 

        return pre[l] / (1 << (n - 1 - r)); 
    } 

    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 1, 0, 1, 0, 1, 1 }; 
        int n = arr.Length; 

        int[] pre = new int[n]; 
        precompute(arr, n, pre); 

        Console.WriteLine(decimalOfSubarr(arr, 
                                        2, 4, n, pre)); 

        Console.WriteLine(decimalOfSubarr(arr, 
                                        4, 5, n, pre)); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php  
// PHP implementation of finding number 
// represented by binary subarray 

// Fills pre[] 
function precompute(&$arr, $n, &$pre) 
{ 
    $pre[$n - 1] = $arr[$n - 1] * pow(2, 0); 
    for ($i = $n - 2; $i >= 0; $i--) 
        $pre[$i] = $pre[$i + 1] + $arr[$i] *  
                           (1 << ($n - 1 - $i)); 
} 

// returns the number represented by  
// a binary subarray l to r 
function decimalOfSubarr(&$arr, $l, $r, $n, &$pre) 
{ 
    // if r is equal to n-1 r+1 does not exist 
    if ($r != $n - 1) 
        return ($pre[$l] - $pre[$r + 1]) /  
                    (1 << ($n - 1 - $r)); 

    return $pre[$l] / (1 << ($n - 1 - $r)); 
} 

// Driver Code 
$arr = array(1, 0, 1, 0, 1, 1 ); 
$n = sizeof($arr); 

$pre = array_fill(0, $n, NULL); 
precompute($arr, $n, $pre); 
echo decimalOfSubarr($arr, 2, 4, $n, $pre) . "\n"; 
echo decimalOfSubarr($arr, 4, 5, $n, $pre) . "\n"; 

// This code is contributed by ita_c 
?> 

```

**输出**：

```
5
3

```

