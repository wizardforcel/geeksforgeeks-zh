# 数组的最小乘积子集

> 原文： [https://www.geeksforgeeks.org/minimum-product-subset-array/](https://www.geeksforgeeks.org/minimum-product-subset-array/)

给定一个数组`a`，我们必须找到数组中存在的元素子集的最小乘积。 最小乘积也可以是单个元素。

**示例**：

```
Input : a[] = { -1, -1, -2, 4, 3 }
Output : -24
Explanation : Minimum product will be ( -2 * -1 * -1 * 4 * 3 ) = -24

Input : a[] = { -1, 0 }
Output : -1
Explanation : -1(single element) is minimum product possible

Input : a[] = { 0, 0, 0 }
Output : 0

```

一个简单的解决方案是[生成所有子集](https://www.geeksforgeeks.org/power-set/)，找到每个子集的乘积并返回最大乘积。

更好的解决方案是使用以下事实。

1.  如果负数为偶数且不为零，则结果为除最大负数之外的所有值的乘积。

2.  如果有奇数个负数而没有零个，那么结果就是所有乘积。

3.  如果有零且为正，没有负，则结果为 0。例外情况是，当没有负数且所有其他元素为正时，我们的结果应为第一小正数。

## C++ 

```cpp

// CPP program to find maximum product of 
// a subset. 
#include <bits/stdc++.h> 
using namespace std; 

int minProductSubset(int a[], int n) 
{ 
    if (n == 1) 
        return a[0]; 

    // Find count of negative numbers, count 
    // of zeros, maximum valued negative number, 
    // minimum valued positive number and product 
    // of non-zero numbers 
    int max_neg = INT_MIN; 
    int min_pos = INT_MAX; 
    int count_neg = 0, count_zero = 0; 
    int prod = 1; 
    for (int i = 0; i < n; i++) { 

        // If number is 0, we don't 
        // multiply it with product. 
        if (a[i] == 0) { 
            count_zero++; 
            continue; 
        } 

        // Count negatives and keep 
        // track of maximum valued negative. 
        if (a[i] < 0) { 
            count_neg++; 
            max_neg = max(max_neg, a[i]); 
        } 

        // Track minimum positive 
        // number of array 
        if (a[i] > 0)  
            min_pos = min(min_pos, a[i]);         

        prod = prod * a[i]; 
    } 

    // If there are all zeros 
    // or no negative number present 
    if (count_zero == n ||  
       (count_neg == 0 && count_zero > 0)) 
        return 0; 

    // If there are all positive 
    if (count_neg == 0) 
        return min_pos; 

    // If there are even number of 
    // negative numbers and count_neg not 0 
    if (!(count_neg & 1) && count_neg != 0) { 

        // Otherwise result is product of 
        // all non-zeros divided by maximum 
        // valued negative. 
        prod = prod / max_neg; 
    } 

    return prod; 
} 

int main() 
{ 
    int a[] = { -1, -1, -2, 4, 3 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << minProductSubset(a, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find maximum product of 
// a subset. 
class GFG { 

    static int minProductSubset(int a[], int n) 
    { 
        if (n == 1) 
            return a[0]; 

        // Find count of negative numbers, 
        // count of zeros, maximum valued  
        // negative number, minimum valued 
        // positive number and product of  
        // non-zero numbers 
        int negmax = Integer.MIN_VALUE; 
        int posmin = Integer.MAX_VALUE; 
        int count_neg = 0, count_zero = 0; 
        int product = 1; 

        for (int i = 0; i < n; i++) 
        { 

            // if number is zero,count it 
            // but dont multiply 
            if(a[i] == 0){ 
                count_zero++; 
                continue; 
            } 

        // count the negetive numbers 
        // and find the max negetive number 
        if(a[i] < 0) 
        { 
                count_neg++; 
                negmax = Math.max(negmax, a[i]); 
            } 

            // find the minimum positive number 
            if(a[i] > 0 && a[i] < posmin) 
            posmin = a[i]; 

            product *= a[i]; 
        } 

        // if there are all zeroes 
        // or zero is present but no  
        // negetive number is present 
        if (count_zero == n ||  
            (count_neg == 0 && count_zero > 0)) 
            return 0; 

        // If there are all positive 
        if (count_neg == 0) 
            return posmin; 

        // If there are even number except  
        // zero of negative numbers  
        if (count_neg % 2 == 0 && count_neg != 0) 
        { 

            // Otherwise result is product of 
            // all non-zeros divided by maximum 
            // valued negative. 
            product = product / negmax; 
        } 

        return product; 
    } 

    // main function  
    public static void main(String[] args) 
    { 

        int a[] = { -1, -1, -2, 4, 3 }; 
        int n = 5; 

        System.out.println(minProductSubset(a, n)); 
    } 
} 

// This code is contributed by Arnab Kundu. 

```

## Python3

```py

# Python3 program to find maximum  
# product of a subset. 

# def to find maximum 
# product of a subset 
def minProductSubset(a, n) :      
    if (n == 1) : 
        return a[0] 

    # Find count of negative numbers, 
    # count of zeros, maximum valued  
    # negative number, minimum valued  
    # positive number and product 
    # of non-zero numbers 
    max_neg = float('-inf') 
    min_pos = float('inf') 
    count_neg = 0
    count_zero = 0
    prod = 1
    for i in range(0,n) : 

        # If number is 0, we don't 
        # multiply it with product. 
        if (a[i] == 0) :      
            count_zero = count_zero + 1
            continue

        # Count negatives and keep 
        # track of maximum valued  
        # negative. 
        if (a[i] < 0) :      
            count_neg = count_neg + 1
            max_neg = max(max_neg, a[i]) 

        # Track minimum positive 
        # number of array 
        if (a[i] > 0) : 
            min_pos = min(min_pos, a[i]) 

        prod = prod * a[i] 

    # If there are all zeros 
    # or no negative number 
    # present 
    if (count_zero == n or (count_neg == 0 
                    and count_zero > 0)) : 
        return 0; 

    # If there are all positive 
    if (count_neg == 0) : 
        return min_pos 

    # If there are even number of 
    # negative numbers and count_neg 
    # not 0 
    if ((count_neg & 1) == 0 and
                       count_neg != 0) : 

        # Otherwise result is product of 
        # all non-zeros divided by  
        # maximum valued negative. 
        prod = int(prod / max_neg) 

    return prod; 

# Driver code 
a = [ -1, -1, -2, 4, 3 ] 
n = len(a) 
print (minProductSubset(a, n)) 
# This code is contributed by  
# Manish Shaw (manishshaw1) 

```

## C# 

```cs

// C# program to find maximum product of 
// a subset. 
using System; 

public class GFG { 

    static int minProductSubset(int[] a, int n) 
    { 
        if (n == 1)  
            return a[0]; 

        // Find count of negative numbers, 
        // count of zeros, maximum valued 
        // negative number, minimum valued 
        // positive number and product of 
        // non-zero numbers 
        int negmax = int.MinValue; 
        int posmin = int.MinValue; 
        int count_neg = 0, count_zero = 0; 
        int product = 1; 

        for (int i = 0; i < n; i++)  
        { 

            // if number is zero, count it 
            // but dont multiply 
            if (a[i] == 0) { 
                count_zero++; 
                continue; 
            } 

            // count the negetive numbers 
            // and find the max negetive number 
            if (a[i] < 0) { 
                count_neg++; 
                negmax = Math.Max(negmax, a[i]); 
            } 

            // find the minimum positive number 
            if (a[i] > 0 && a[i] < posmin) { 
                posmin = a[i]; 
            } 

            product *= a[i]; 
        } 

        // if there are all zeroes 
        // or zero is present but no 
        // negetive number is present 
        if (count_zero == n || (count_neg == 0  
                             && count_zero > 0)) 
            return 0; 

        // If there are all positive 
        if (count_neg == 0)  
            return posmin; 

        // If there are even number except 
        // zero of negative numbers 
        if (count_neg % 2 == 0 && count_neg != 0) 
        { 

            // Otherwise result is product of 
            // all non-zeros divided by maximum 
            // valued negative. 
            product = product / negmax; 
        } 

        return product; 
    } 

    // main function 
    public static void Main() 
    { 

        int[] a = new int[] { -1, -1, -2, 4, 3 }; 
        int n = 5; 

        Console.WriteLine(minProductSubset(a, n)); 
    } 
} 

// This code is contributed by Ajit. 

```

## PHP

```php

<?php 
// PHP program to find maximum  
// product of a subset. 

// Function to find maximum 
// product of a subset 
function minProductSubset($a, $n) 
{ 

    if ($n == 1) 
        return $a[0]; 

    // Find count of negative numbers, 
    // count of zeros, maximum valued  
    // negative number, minimum valued  
    // positive number and product 
    // of non-zero numbers 
    $max_neg = PHP_INT_MIN; 
    $min_pos = PHP_INT_MAX; 
    $count_neg = 0; $count_zero = 0; 
    $prod = 1; 
    for ($i = 0; $i < $n; $i++)  
    { 

        // If number is 0, we don't 
        // multiply it with product. 
        if ($a[$i] == 0)  
        { 
            $count_zero++; 
            continue; 
        } 

        // Count negatives and keep 
        // track of maximum valued  
        // negative. 
        if ($a[$i] < 0) 
        { 
            $count_neg++; 
            $max_neg = max($max_neg, $a[$i]); 
        } 

        // Track minimum positive 
        // number of array 
        if ($a[$i] > 0)  
            $min_pos = min($min_pos, $a[$i]);  

        $prod = $prod * $a[$i]; 
    } 

    // If there are all zeros 
    // or no negative number 
    // present 
    if ($count_zero == $n ||  
       ($count_neg == 0 &&  
        $count_zero > 0)) 
        return 0; 

    // If there are all positive 
    if ($count_neg == 0) 
        return $min_pos; 

    // If there are even number of 
    // negative numbers and count_neg 
    // not 0 
    if (!($count_neg & 1) &&  
          $count_neg != 0) 
    { 

        // Otherwise result is product of 
        // all non-zeros divided by maximum 
        // valued negative. 
        $prod = $prod / $max_neg; 
    } 

    return $prod; 
} 

// Driver code 
$a = array( -1, -1, -2, 4, 3 ); 
$n = sizeof($a); 
echo(minProductSubset($a, $n)); 

// This code is contributed by Ajit. 
?> 

```

**输出**：

```
-24

```

时间复杂度：`O(n)`。

辅助空间：`O(1)`。



* * *

* * *



