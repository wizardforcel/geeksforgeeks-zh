# 范围在`(a[i], a[j])`中，可被`x`整除的`k`个数字的偶对数量（`a[j] >= a[i]`）

> 原文： [https://www.geeksforgeeks.org/no-pairs-aj-ai-k-numbers-range-ai-aj-divisible-x/](https://www.geeksforgeeks.org/no-pairs-aj-ai-k-numbers-range-ai-aj-divisible-x/)

给定一个数组和两个数字`x`和`k`。 找出索引`(i, j)`的不同有序对的数量，使得`a[j] >= a[i]`，并且正好有`k`个整数`num`，使得`num`可被`x`整除，并且`num`在`a[i] - a[j]`范围内。

**示例**：

```
Input : arr[] = {1, 3, 5, 7}
        x = 2, k = 1
Output : 3 
Explanation: The pairs (1, 3), (3, 5) and (5, 7) 
have k (which is 1) integers i.e., 2, 4, 6 
respectively for every pair in between them.

Input  : arr[] = {5, 3, 1, 7} 
         x = 2, k = 0 
Output : 4 
Explanation: The pairs with indexes (1, 1), (2, 2),
(3, 3), (4, 4)  have k = 0 integers that are 
divisible by 2 in between them.

```



**朴素方法**会遍历所有可能的对，并计算在它们之间具有`k`个整数的对数，这些整数可被`x`整除。

**时间复杂度**：`O(n ^ 2)`。

**有效方法**是对数组进行排序，然后使用[二分搜索](https://www.geeksforgeeks.org/binary-search/)找出数字的左右边界（使用[`lower_bound`函数](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/)内置函数可以做到） 满足条件而哪些不满足。 我们必须对数组进行排序，因为给出的每对数组均应为`a[j] >= a[i]`，而与`i`和`j`的值无关。 排序后，我们遍历`n`个元素，并找到与`x`相乘得到`a[i] - 1`的数字，以便我们可以通过将`d`加到`d = a [i] - 1 / x`来找到`k`个数。 因此，我们对值`(d + k) * x `进行二分搜索，以获取可以构成一对`a[i]`的倍数，因为它将在`a[i]`和`a[j]`之间恰好有`k`个整数。 这样，我们在`O(log n)`中使用二分搜索获得`a[j]`的左边界，对于所有其他可能使用`a[i]`的对，我们需要通过搜索等于或大于`(d + k + 1) * x`的数来找出最右边界，在这里我们将得到`k + 1`倍，并且我们得到了对数（作为（右减去左）的边界）。

## C++ 

```cpp

// cpp program to calculate the number 
// pairs satisfying th condition 
#include <bits/stdc++.h> 
using namespace std; 

// function to calculate the number of pairs 
int countPairs(int a[], int n, int x, int k) 
{ 
    sort(a, a + n);     

    // traverse through all elements 
    int ans = 0; 
    for (int i = 0; i < n; i++) { 

        // current number's divisor 
        int d = (a[i] - 1) / x; 

        // use binary search to find the element  
        // after k multiples of x 
        int it1 = lower_bound(a, a + n,  
                         max((d + k) * x, a[i])) - a; 

        // use binary search to find the element 
        // after k+1 multiples of x so that we get  
        // the answer bu subtracting 
        int it2 = lower_bound(a, a + n, 
                     max((d + k + 1) * x, a[i])) - a; 

        // the difference of index will be the answer 
        ans += it2 - it1; 
    } 
    return ans; 
} 

// driver code to check the above fucntion 
int main() 
{ 
    int a[] = { 1, 3, 5, 7 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    int x = 2, k = 1; 

    // function call to get the number of pairs 
    cout << countPairs(a, n, x, k); 
    return 0; 
} 

```

## Java

```java

// Java program to calculate the number 
// pairs satisfying th condition 
import java.util.*;  

class GFG 
{ 

// function to calculate the number of pairs 
static int countPairs(int a[], int n, int x, int k) 
{ 
    Arrays.sort(a);  

    // traverse through all elements 
    int ans = 0; 
    for (int i = 0; i < n; i++)  
    { 

        // current number's divisor 
        int d = (a[i] - 1) / x; 

        // use binary search to find the element  
        // after k multiples of x 
        int it1 = Arrays.binarySearch(a,  
                    Math.max((d + k) * x, a[i])); 

        // use binary search to find the element 
        // after k+1 multiples of x so that we get  
        // the answer bu subtracting 
        int it2 = Arrays.binarySearch(a, 
                    Math.max((d + k + 1) * x, a[i])) ; 

        // the difference of index will be the answer 
        ans += it1 - it2; 
    } 
    return ans; 
} 

// Driver code  
public static void main(String[] args) 
{ 
    int []a = { 1, 3, 5, 7 }; 
    int n = a.length; 
    int x = 2, k = 1; 

    // function call to get the number of pairs 
    System.out.println(countPairs(a, n, x, k)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python program to calculate the number 
# pairs satisfying th condition 

import bisect 

# function to calculate the number of pairs 
def countPairs(a, n, x, k): 
    a.sort() 

    # traverse through all elements 
    ans = 0
    for i in range(n): 

        # current number's divisor 
        d = (a[i] - 1) // x 

        # use binary search to find the element 
        # after k multiples of x 
        it1 = bisect.bisect_left(a, max((d + k) * x, a[i])) 

        # use binary search to find the element 
        # after k+1 multiples of x so that we get 
        # the answer bu subtracting 
        it2 = bisect.bisect_left(a, max((d + k + 1) * x, a[i])) 

        # the difference of index will be the answer 
        ans += it2 - it1 

    return ans 

# Driver code 
if __name__ == "__main__": 
    a = [1, 3, 5, 7] 
    n = len(a) 
    x = 2
    k = 1

    # function call to get the number of pairs 
    print(countPairs(a, n, x, k)) 

# This code is contributed by 
# sanjeev2552 

```

**输出**：

```
3

```

**时间复杂度**：`O(N log N)`。



* * *

* * *



