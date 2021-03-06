# 检查数组是否排序的程序（迭代和递归）

> 原文： [https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)

给定大小为`n`的数组，编写一个程序来检查它是否按升序排序。 数组中允许相等值，并且认为两个连续的相等值已排序。

**示例**：

```
Input : 20 21 45 89 89 90
Output : Yes

Input : 20 20 45 89 89 90
Output : Yes

Input : 20 20 78 98 99 97
Output : No

```



**递归方法**：

递归方法的基本思想：

```
1: If size of array is zero or one, return true.
2: Check last two elements of array, if they are
   sorted, perform a recursive call with n-1
   else, return false.
If all the elements will be found sorted, n will
eventually fall to one, satisfying Step 1.

```

下面是使用递归的实现：

## C++ 

```cpp

// Recursive approach to check if an 
// Array is sorted or not 
#include <bits/stdc++.h> 
using namespace std; 

// Function that returns 0 if a pair 
// is found unsorted 
int arraySortedOrNot(int arr[], int n) 
{ 
    // Array has one or no element or the 
    // rest are already checked and approved. 
    if (n == 1 || n == 0) 
        return 1; 

    // Unsorted pair found (Equal values allowed) 
    if (arr[n - 1] < arr[n - 2]) 
        return 0; 

    // Last pair was sorted 
    // Keep on checking 
    return arraySortedOrNot(arr, n - 1); 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 20, 23, 23, 45, 78, 88 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    if (arraySortedOrNot(arr, n)) 
        cout << "Yes\n"; 
    else
        cout << "No\n"; 
} 

```

## Java

```java

// Recursive approach to check if an 
// Array is sorted or not 

class CkeckSorted { 
    // Function that returns 0 if a pair 
    // is found unsorted 
    static int arraySortedOrNot(int arr[], int n) 
    { 
        // Array has one or no element or the 
        // rest are already checked and approved. 
        if (n == 1 || n == 0) 
            return 1; 

        // Unsorted pair found (Equal values allowed) 
        if (arr[n - 1] < arr[n - 2]) 
            return 0; 

        // Last pair was sorted 
        // Keep on checking 
        return arraySortedOrNot(arr, n - 1); 
    } 

    // main function 
    public static void main(String[] args) 
    { 
        int arr[] = { 20, 23, 23, 45, 78, 88 }; 
        int n = arr.length; 
        if (arraySortedOrNot(arr, n) != 0) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 

```

## Python3

```py

# Recursive approach to check if an 
# Array is sorted or not 

# Function that returns 0 if a pair 
# is found unsorted 
def arraySortedOrNot(arr): 

    # Calculating length 
    n = len(arr) 

    # Array has one or no element or the 
    # rest are already checked and approved. 
    if n == 1 or n == 0: 
        return True

    # Recursion applied till last element 
    return arr[0]<= arr[1] and arraySortedOrNot(arr[1:]) 

arr = [20, 23, 23, 45, 78, 88] 

# Displaying result 
if arraySortedOrNot(arr): print("Yes") 
else: print("No")  

```

## C# 

```cs

// Recursive approach to check if an 
// Array is sorted or not 
using System; 

class CkeckSorted 
{ 
    // Function that returns 0 if a pair 
    // is found unsorted 
    static int arraySortedOrNot(int []arr, int n) 
    { 
        // Array has one or no element or the 
        // rest are already checked and approved. 
        if (n == 1 || n == 0) 
            return 1; 

        // Unsorted pair found (Equal values allowed) 
        if (arr[n - 1] < arr[n - 2]) 
            return 0; 

        // Last pair was sorted 
        // Keep on checking 
        return arraySortedOrNot(arr, n - 1); 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        int []arr = { 20, 23, 23, 45, 78, 88 }; 
        int n = arr.Length; 
        if (arraySortedOrNot(arr, n) != 0) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
Yes

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`用于递归调用栈。

**迭代方法**：想法几乎相同。 迭代方法的好处是它避免了使用递归栈空间和递归开销。

下面是使用迭代的实现：

## C++

```cpp

// C++ program to check if an 
// Array is sorted or not 
#include <bits/stdc++.h> 
using namespace std; 

// Function that returns true if array is 
// sorted in non-decreasing order. 
bool arraySortedOrNot(int arr[], int n) 
{ 
    // Array has one or no element 
    if (n == 0 || n == 1) 
        return true; 

    for (int i = 1; i < n; i++) 

        // Unsorted pair found 
        if (arr[i - 1] > arr[i]) 
            return false; 

    // No unsorted pair found 
    return true; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 20, 23, 23, 45, 78, 88 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    if (arraySortedOrNot(arr, n)) 
        cout << "Yes\n"; 
    else
        cout << "No\n"; 
} 

```

## Java

```java

// Recursive approach to check if an 
// Array is sorted or not 
class GFG { 

    // Function that returns true if array is 
    // sorted in non-decreasing order. 
    static boolean arraySortedOrNot(int arr[], int n) 
    { 

        // Array has one or no element 
        if (n == 0 || n == 1) 
            return true; 

        for (int i = 1; i < n; i++) 

            // Unsorted pair found 
            if (arr[i - 1] > arr[i]) 
                return false; 

        // No unsorted pair found 
        return true; 
    } 

    // driver code 
    public static void main(String[] args) 
    { 

        int arr[] = { 20, 23, 23, 45, 78, 88 }; 
        int n = arr.length; 

        if (arraySortedOrNot(arr, n)) 
            System.out.print("Yes\n"); 
        else
            System.out.print("No\n"); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python3 program to check if an 
# Array is sorted or not 

# Function that returns true if array is 
# sorted in non-decreasing order. 
def arraySortedOrNot(arr, n): 

    # Array has one or no element 
    if (n == 0 or n == 1): 
        return True

    for i in range(1, n): 

        # Unsorted pair found 
        if (arr[i-1] > arr[i]): 
            return False

    # No unsorted pair found 
    return True

# Driver code 
arr = [20, 23, 23, 45, 78, 88] 
n = len(arr) 
if (arraySortedOrNot(arr, n)): 
    print("Yes") 
else: 
    print("No") 

# This code is contributed by Anant Agarwal. 

```

## C#

```cs

// Recursive approach to check if an 
// Array is sorted or not 
using System; 

class GFG 
{ 

    // Function that returns true if array is 
    // sorted in non-decreasing order. 
    static bool arraySortedOrNot(int []arr, int n) 
    { 

        // Array has one or no element 
        if (n == 0 || n == 1) 
            return true; 

        for (int i = 1; i < n; i++) 

            // Unsorted pair found 
            if (arr[i - 1] > arr[i]) 
                return false; 

        // No unsorted pair found 
        return true; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        int []arr = { 20, 23, 23, 45, 78, 88 }; 
        int n = arr.Length; 

        if (arraySortedOrNot(arr, n)) 
            Console.Write("Yes\n"); 
        else
            Console.Write("No\n"); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
Yes
```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(1)`。

