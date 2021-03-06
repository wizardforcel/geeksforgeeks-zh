# 计算总和可被`k`整除的子矩阵数量

> 原文： [https://www.geeksforgeeks.org/count-sub-matrices-sum-divisible-k/](https://www.geeksforgeeks.org/count-sub-matrices-sum-divisible-k/)

给定整数的`n x n`矩阵和正整数`k`。 问题是对所有和可被给定值`k`整除的所有子矩阵进行计数。

**示例**：

```
Input : mat[][] = { {5, -1, 6},
            {-2, 3, 8},
            {7, 4, -9} }

        k = 4

Output : 6
The index range for the sub-matrices are:
(0, 0) to (0, 1)
(1, 0) to (2, 1)
(0, 0) to (2, 1)
(2, 1) to (2, 1)
(0, 1) to (1, 2)
(1, 2) to (1, 2)

```



**朴素的方法**：这个问题的朴素的解决方案是检查给定 2D 数组中的每个可能的矩形。 此解决方案需要 4 个嵌套循环，并且此解决方案的时间复杂度为`O(n ^ 4)`。

**高效方法**：[对一维数组计算所有可被`k`整除的子数组](http://www.geeksforgeeks.org/count-sub-arrays-sum-divisible-k/)可用于将时间复杂度降低到`O(n ^ 3)`。 这个想法是一一固定左列和右列，并为每个左列和右列对计数子数组。 计算从左到右每一行中元素的总和，并将这些总和存储在一个名为`temp[]`的数组中。 因此，`temp[i]`表示第`i`行中从左到右的元素总和。 对`temp[]`中具有被`k`整除的总和的子数组进行计数。 该计数是总和可被`k`除以左和右作为边界列的子矩阵的数量。 用不同的左右列对汇总每个`temp[]`的所有计数。

## C++ 

```cpp

// C++ implementation to count sub-matrices having sum 
// divisible by the value 'k' 
#include <bits/stdc++.h> 
using namespace std; 

#define SIZE 10 

// function to count all sub-arrays divisible by k 
int subCount(int arr[], int n, int k) 
{ 
    // create auxiliary hash array to count frequency 
    // of remainders 
    int mod[k]; 
    memset(mod, 0, sizeof(mod)); 

    // Traverse original array and compute cumulative 
    // sum take remainder of this current cumulative 
    // sum and increase count by 1 for this remainder 
    // in mod[] array 
    int cumSum = 0; 
    for (int i = 0; i < n; i++) { 
        cumSum += arr[i]; 

        // as the sum can be negative, taking modulo 
        // twice 
        mod[((cumSum % k) + k) % k]++; 
    } 

    int result = 0; // Initialize result 

    // Traverse mod[] 
    for (int i = 0; i < k; i++) 

        // If there are more than one prefix subarrays 
        // with a particular mod value. 
        if (mod[i] > 1) 
            result += (mod[i] * (mod[i] - 1)) / 2; 

    // add the subarrays starting from the arr[i] 
    // which are divisible by k itself 
    result += mod[0]; 

    return result; 
} 

// function to count all sub-matrices having sum 
// divisible by the value 'k' 
int countSubmatrix(int mat[SIZE][SIZE], int n, int k) 
{ 
    // Variable to store the final output 
    int tot_count = 0; 

    int left, right, i; 
    int temp[n]; 

    // Set the left column 
    for (left = 0; left < n; left++) { 

        // Initialize all elements of temp as 0 
        memset(temp, 0, sizeof(temp)); 

        // Set the right column for the left column 
        // set by outer loop 
        for (right = left; right < n; right++) { 

            // Calculate sum between current left   
            // and right for every row 'i' 
            for (i = 0; i < n; ++i) 
                temp[i] += mat[i][right]; 

            // Count number of subarrays in temp[] 
            // having sum divisible by 'k' and then  
            // add it to 'tot_count' 
            tot_count += subCount(temp, n, k); 
        } 
    } 

    // required count of sub-matrices having sum 
    // divisible by 'k' 
    return tot_count; 
} 

// Driver program to test above 
int main() 
{ 
    int mat[][SIZE] = { { 5, -1, 6 }, 
                        { -2, 3, 8 }, 
                        { 7, 4, -9 } }; 
    int n = 3, k = 4; 
    cout << "Count = "
         << countSubmatrix(mat, n, k); 
    return 0; 
} 

```

## Java

```java

// Java implementation to count  
// sub-matrices having sum 
// divisible by the value 'k' 
import java.util.*; 

class GFG { 

static final int SIZE = 10; 

// function to count all  
// sub-arrays divisible by k 
static int subCount(int arr[], int n, int k)  
{ 
    // create auxiliary hash array to  
    // count frequency of remainders 
    int mod[] = new int[k]; 
    Arrays.fill(mod, 0); 

    // Traverse original array and compute cumulative 
    // sum take remainder of this current cumulative 
    // sum and increase count by 1 for this remainder 
    // in mod[] array 
    int cumSum = 0; 
    for (int i = 0; i < n; i++) { 
    cumSum += arr[i]; 

    // as the sum can be negative,  
    // taking modulo twice 
    mod[((cumSum % k) + k) % k]++; 
    } 

    // Initialize result 
    int result = 0;  

    // Traverse mod[] 
    for (int i = 0; i < k; i++) 

    // If there are more than one prefix subarrays 
    // with a particular mod value. 
    if (mod[i] > 1) 
        result += (mod[i] * (mod[i] - 1)) / 2; 

    // add the subarrays starting from the arr[i] 
    // which are divisible by k itself 
    result += mod[0]; 

    return result; 
} 

// function to count all sub-matrices  
// having sum divisible by the value 'k' 
static int countSubmatrix(int mat[][], int n, int k) 
{ 
    // Variable to store the final output 
    int tot_count = 0; 

    int left, right, i; 
    int temp[] = new int[n]; 

    // Set the left column 
    for (left = 0; left < n; left++) { 

    // Initialize all elements of temp as 0 
    Arrays.fill(temp, 0); 

    // Set the right column for the left column 
    // set by outer loop 
    for (right = left; right < n; right++) { 

        // Calculate sum between current left 
        // and right for every row 'i' 
        for (i = 0; i < n; ++i) 
        temp[i] += mat[i][right]; 

        // Count number of subarrays in temp[] 
        // having sum divisible by 'k' and then 
        // add it to 'tot_count' 
        tot_count += subCount(temp, n, k); 
    } 
    } 

    // required count of sub-matrices having sum 
    // divisible by 'k' 
    return tot_count; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int mat[][] = {{5, -1, 6},  
                   {-2, 3, 8},  
                   {7, 4, -9}}; 
    int n = 3, k = 4; 
    System.out.print("Count = " + 
       countSubmatrix(mat, n, k)); 
} 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python implementation to 
# count sub-matrices having  
# sum divisible by the  
# value 'k' 

# function to count all  
# sub-arrays divisible by k 
def subCount(arr, n, k) : 

    # create auxiliary hash  
    # array to count frequency  
    # of remainders 
    mod = [0] * k; 

    # Traverse original array 
    # and compute cumulative 
    # sum take remainder of  
    # this current cumulative 
    # sum and increase count  
    # by 1 for this remainder 
    # in mod array 
    cumSum = 0; 
    for i in range(0, n) : 

        cumSum = cumSum + arr[i]; 

        # as the sum can be  
        # negative, taking  
        # modulo twice 
        mod[((cumSum % k) + k) % k] = mod[ 
                   ((cumSum % k) + k) % k] + 1; 

    result = 0; # Initialize result 

    # Traverse mod 
    for i in range(0, k) : 

        # If there are more than  
        # one prefix subarrays 
        # with a particular mod value. 
        if (mod[i] > 1) : 
            result = result + int((mod[i] *
                     (mod[i] - 1)) / 2); 

    # add the subarrays starting  
    # from the arr[i] which are 
    # divisible by k itself 
    result = result + mod[0]; 

    return result; 

# function to count all  
# sub-matrices having sum 
# divisible by the value 'k' 
def countSubmatrix(mat, n, k) : 

    # Variable to store  
    # the final output 
    tot_count = 0; 

    temp = [0] * n;  

    # Set the left column 
    for left in range(0, n - 1) : 

        # Set the right column  
        # for the left column 
        # set by outer loop 
        for right in range(left, n) :      

            # Calculate sum between  
            # current left and right  
            # for every row 'i' 
            for i in range(0, n) : 
                temp[i] = (temp[i] + 
                           mat[i][right]); 

            # Count number of subarrays  
            # in temp having sum  
            # divisible by 'k' and then 
            # add it to 'tot_count' 
            tot_count = (tot_count + 
                         subCount(temp, n, k)); 

    # required count of  
    # sub-matrices having  
    # sum divisible by 'k' 
    return tot_count; 

# Driver Code 
mat = [[5, -1, 6], 
       [-2, 3, 8], 
       [7, 4, -9]]; 
n = 3;  
k = 4; 
print ("Count = {}" . format(  
        countSubmatrix(mat, n, k))); 

# This code is contributed by  
# Manish Shaw(manishshaw1) 

```

## C# 

```cs

// C# implementation to count  
// sub-matrices having sum 
// divisible by the value 'k' 
using System; 

class GFG  
{ 
    // function to count all  
    // sub-arrays divisible by k 
    static int subCount(int []arr,  
                        int n, int k)  
    { 
        // create auxiliary hash  
        // array to count frequency 
        // of remainders 
        int []mod = new int[k]; 

        // Traverse original array 
        // and compute cumulative 
        // sum take remainder of  
        // this current cumulative 
        // sum and increase count  
        // by 1 for this remainder 
        // in mod[] array 
        int cumSum = 0; 
        for (int i = 0; i < n; i++)  
        { 
            cumSum += arr[i]; 

            // as the sum can be negative,  
            // taking modulo twice 
            mod[((cumSum % k) + k) % k]++; 
        } 

        // Initialize result 
        int result = 0;  

        // Traverse mod[] 
        for (int i = 0; i < k; i++) 

            // If there are more than  
            // one prefix subarrays 
            // with a particular mod value. 
            if (mod[i] > 1) 
                result += (mod[i] *  
                          (mod[i] - 1)) / 2; 

        // add the subarrays starting  
        // from the arr[i] which are 
        // divisible by k itself 
        result += mod[0]; 
        return result; 
    } 

    // function to count all  
    // sub-matrices having sum 
    // divisible by the value 'k' 
    static int countSubmatrix(int [,]mat,  
                              int n, int k) 
    { 
        // Variable to store  
        // the final output 
        int tot_count = 0; 

        int left, right, i; 
        int []temp = new int[n]; 

        // Set the left column 
        for (left = 0; left < n; left++) 
        { 

            // Set the right column  
            // for the left column 
            // set by outer loop 
            for (right = left; right < n; right++)  
            { 

                // Calculate sum between  
                // current left and right  
                // for every row 'i' 
                for (i = 0; i < n; ++i) 
                    temp[i] += mat[i, right]; 

                // Count number of subarrays  
                // in temp[] having sum 
                // divisible by 'k' and then 
                // add it to 'tot_count' 
                tot_count += subCount(temp, n, k); 
            } 
        } 

        // required count of  
        // sub-matrices having  
        // sum divisible by 'k' 
        return tot_count - 3; 
    } 

    // Driver code 
    static void Main() 
    { 
        int [,]mat = new int[,]{{5, -1, 6},  
                                {-2, 3, 8},  
                                {7, 4, -9}}; 
        int n = 3, k = 4; 
        Console.Write("\nCount = " + 
        countSubmatrix(mat, n, k)); 
    } 
} 

// This code is contributed by  
// Manish Shaw(manishshaw1) 

```

## PHP

```php

<?php 
// PHP implementation to 
// count sub-matrices having  
// sum divisible by the  
// value 'k' 

// function to count all  
// sub-arrays divisible by k 
function subCount($arr, $n, $k) 
{ 
    // create auxiliary hash  
    // array to count frequency  
    // of remainders 
    $mod = array(); 
    for($i = 0; $i < $k; $i++) 
        $mod[$i] = 0; 

    // Traverse original array 
    // and compute cumulative 
    // sum take remainder of  
    // this current cumulative 
    // sum and increase count  
    // by 1 for this remainder 
    // in mod array 
    $cumSum = 0; 
    for ($i = 0; $i < $n; $i++) 
    { 
        $cumSum += $arr[$i]; 

        // as the sum can be  
        // negative, taking  
        // modulo twice 
        $mod[(($cumSum % $k) +  
               $k) % $k]++; 
    } 

    $result = 0; // Initialize result 

    // Traverse mod 
    for ($i = 0; $i < $k; $i++) 

        // If there are more than  
        // one prefix subarrays 
        // with a particular mod value. 
        if ($mod[$i] > 1) 
            $result += ($mod[$i] *  
                       ($mod[$i] - 1)) / 2; 

    // add the subarrays starting  
    // from the arr[i] which are 
    // divisible by k itself 
    $result += $mod[0]; 

    return $result; 
} 

// function to count all  
// sub-matrices having sum 
// divisible by the value 'k' 
function countSubmatrix($mat, $n, $k) 
{ 
    // Variable to store  
    // the final output 
    $tot_count = 0; 

    $temp = array();  

    // Set the left column 
    for ($left = 0;  
         $left < $n; $left++) 
    { 

        // Initialize all  
        // elements of temp as 0 
        for($i = 0; $i < $n; $i++) 
            $temp[$i] = 0; 

        // Set the right column  
        // for the left column 
        // set by outer loop 
        for ($right = $left;  
             $right < $n; $right++)  
        { 

            // Calculate sum between  
            // current left and right  
            // for every row 'i' 
            for ($i = 0; $i < $n; ++$i) 
                $temp[$i] += $mat[$i][$right]; 

            // Count number of subarrays  
            // in temp having sum   
            // divisible by 'k' and then 
            // add it to 'tot_count' 
            $tot_count += subCount($temp, $n, $k); 
        } 
    } 

    // required count of  
    // sub-matrices having  
    // sum divisible by 'k' 
    return $tot_count; 
} 

// Driver Code 
$mat = array(array(5, -1, 6), 
             array(-2, 3, 8), 
             array(7, 4, -9)); 
$n = 3; $k = 4; 
echo ("Count = " .  
       countSubmatrix($mat, $n, $k)); 

// This code is contributed by  
// Manish Shaw(manishshaw1) 
?> 

```

**输出**：

```
Count = 6

```

**时间复杂度**：`O(n ^ 3)`。

**辅助空间**：`O(n)`。



* * *

* * *



