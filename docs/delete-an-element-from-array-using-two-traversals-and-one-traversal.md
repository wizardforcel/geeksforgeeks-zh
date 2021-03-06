# 从数组中删除一个元素（使用两次遍历和一次遍历）

> 原文： [https://www.geeksforgeeks.org/delete-an-element-from-array-using-two-traversals-and-one-traversal/](https://www.geeksforgeeks.org/delete-an-element-from-array-using-two-traversals-and-one-traversal/)

给定一个数组和一个数字`x`，编写一个函数从给定的数组中删除`x`。 我们假设数组维护着两件事，容量和大小。 因此，当我们删除一个项目时，容量不会改变，只有大小会改变。

**示例**：

```
Input:  arr[] = {3, 1, 2, 5, 90}, x = 2, size = 5, capacity = 5
Output: arr[] = {3, 1, 5, 90, _}, size = 4, capacity = 5

Input:  arr[] = {3, 1, 2, _, _}, x = 2, size = 3, capacity = 5
Output: arr[] = {3, 1, _, _, _}, size = 4, capacity = 5

```

**方法 1（先搜索，然后删除）**：

我们首先在数组中搜索`x`，然后在`x`右侧的元素向后搜索一个位置。 以下是此简单方法的实现。

## C/C++ 

```

// C++ program to remove a given element from an array 
#include<bits/stdc++.h> 
using namespace std; 

// This function removes an element x from arr[] and 
// returns new size after removal (size is reduced only 
// when x is present in arr[] 
int deleteElement(int arr[], int n, int x) 
{ 
   // Search x in array 
   int i; 
   for (i=0; i<n; i++) 
      if (arr[i] == x) 
         break; 

   // If x found in array 
   if (i < n) 
   { 
     // reduce size of array and move all 
     // elements on space ahead 
     n = n - 1; 
     for (int j=i; j<n; j++) 
        arr[j] = arr[j+1]; 
   } 

   return n; 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[] = {11, 15, 6, 8, 9, 10}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int x = 6; 

    // Delete x from arr[] 
    n = deleteElement(arr, n, x); 

    cout << "Modified array is \n"; 
    for (int i=0; i<n; i++) 
       cout << arr[i] << " "; 

    return 0; 
} 

```

## Java

```java

// Java program to remove a given element from an array 
import java.io.*; 

class Deletion { 

    // This function removes an element x from arr[] and 
    // returns new size after removal (size is reduced only 
    // when x is present in arr[] 
    static int deleteElement(int arr[], int n, int x) 
    { 
        // Search x in array 
        int i; 
        for (i=0; i<n; i++) 
            if (arr[i] == x) 
                break; 

        // If x found in array 
        if (i < n) 
        { 
            // reduce size of array and move all 
            // elements on space ahead 
            n = n - 1; 
            for (int j=i; j<n; j++) 
                arr[j] = arr[j+1]; 
        } 

        return n; 
    } 

    // Driver program to test above function 
    public static void main(String[] args) 
    { 
        int arr[] = {11, 15, 6, 8, 9, 10}; 
        int n = arr.length; 
        int x = 6; 

        // Delete x from arr[] 
        n = deleteElement(arr, n, x); 

        System.out.println("Modified array is"); 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i]+" "); 

    } 
} 
/*This code is contributed by Devesh Agrawal*/

```

## Python3

```py

# Python 3 program to remove a given  
# element from an array 

# This function removes an element x  
# from arr[] and returns new size after  
# removal (size is reduced only when x  
# is present in arr[] 
def deleteElement(arr, n, x): 

    # Search x in array 
    for i in range(n): 
        if (arr[i] == x): 
            break

    # If x found in array 
    if (i < n): 

        # reduce size of array and move  
        # all elements on space ahead 
        n = n - 1; 
        for j in range(i, n, 1): 
            arr[j] = arr[j + 1] 

    return n 

# Driver Code 
if __name__ == '__main__': 
    arr = [11, 15, 6, 8, 9, 10] 
    n = len(arr) 
    x = 6

    # Delete x from arr[] 
    n = deleteElement(arr, n, x) 

    print("Modified array is") 
    for i in range(n): 
        print(arr[i], end = " ") 

# This code is contributed by 
# Shashank_Sharma 

```

## C# 

```cs

// C# program to remove a given element from 
// an array 
using System; 

class GFG { 

    // This function removes an element x 
    // from arr[] and returns new size  
    // after removal (size is reduced only 
    // when x is present in arr[] 
    static int deleteElement(int []arr, 
                              int n, int x) 
    { 

        // Search x in array 
        int i; 
        for (i = 0; i < n; i++) 
            if (arr[i] == x) 
                break; 

        // If x found in array 
        if (i < n) 
        { 

            // reduce size of array and 
            // move all elements on  
            // space ahead 
            n = n - 1; 
            for (int j = i; j < n; j++) 
                arr[j] = arr[j+1]; 
        } 

        return n; 
    } 

    // Driver program to test above function 
    public static void Main() 
    { 
        int []arr = {11, 15, 6, 8, 9, 10}; 
        int n = arr.Length; 
        int x = 6; 

        // Delete x from arr[] 
        n = deleteElement(arr, n, x); 

        Console.WriteLine("Modified array is"); 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i]+" "); 

    } 
} 

// This code is contributed by nitin mittal. 

```

**输出**：

```
Modified array is
11 15 8 9 10
```

**方法 2（在搜索时移动元素）**：

此方法假定元素始终存在于数组中。 这个想法是从最右边的元素开始，并在搜索`x`时保持元素不断移动。 以下是此方法的 C++ 和 Java 实现。 请注意，当数组中不存在`x`时，此方法可能会产生意外结果。

## C++ 

```cpp

// C++ program to remove a given element from an array 
#include<iostream> 
using namespace std; 

// This function removes an element x from arr[] and 
// returns new size after removal. 
// Returned size is n-1 when element is present. 
// Otherwise 0 is returned to indicate failure. 
int deleteElement(int arr[], int n, int x) 
{ 
   // If x is last element, nothing to do 
   if (arr[n-1] == x) 
       return (n-1); 

   // Start from rightmost element and keep moving 
   // elements one position ahead. 
   int prev = arr[n-1], i; 
   for (i=n-2; i>=0 && arr[i]!=x; i--) 
   { 
       int curr = arr[i]; 
       arr[i] = prev; 
       prev = curr; 
   } 

   // If element was not found 
   if (i < 0) 
     return 0; 

   // Else move the next element in place of x 
   arr[i] = prev; 

   return (n-1); 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[] = {11, 15, 6, 8, 9, 10}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int x = 6; 

    // Delete x from arr[] 
    n = deleteElement(arr, n, x); 

    cout << "Modified array is \n"; 
    for (int i=0; i<n; i++) 
       cout << arr[i] << " "; 

    return 0; 
} 

```

## Java

```java

// Java program to remove a given element from an array 
import java.io.*; 

class Deletion 
{ 
    // This function removes an element x from arr[] and 
    // returns new size after removal. 
    // Returned size is n-1 when element is present. 
    // Otherwise 0 is returned to indicate failure. 
    static int deleteElement(int arr[], int n, int x) 
    { 
        // If x is last element, nothing to do 
        if (arr[n-1] == x) 
            return (n-1); 

        // Start from rightmost element and keep moving 
        // elements one position ahead. 
        int prev = arr[n-1], i; 
        for (i=n-2; i>=0 && arr[i]!=x; i--) 
        { 
            int curr = arr[i]; 
            arr[i] = prev; 
            prev = curr; 
        } 

        // If element was not found 
        if (i < 0) 
            return 0; 

        // Else move the next element in place of x 
        arr[i] = prev; 

        return (n-1); 
    } 

    // Driver program to test above function 
    public static void main(String[] args) 
    { 
        int arr[] = {11, 15, 6, 8, 9, 10}; 
        int n = arr.length; 
        int x = 6; 

        // Delete x from arr[] 
        n = deleteElement(arr, n, x); 

        System.out.println("Modified array is"); 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i]+" "); 

    } 
} 
/*This code is contributed by Devesh Agrawal*/

```

## Python3

```py

# python program to remove a given element from an array  

# This function removes an element x from arr[] and  
# returns new size after removal.  
# Returned size is n-1 when element is present.  
# Otherwise 0 is returned to indicate failure.  
def deleteElement(arr,n,x): 

    # If x is last element, nothing to do  
    if arr[n-1]==x: 
        return n-1

    # Start from rightmost element and keep moving  
   # elements one position ahead.  

    prev = arr[n-1] 
    for i in range(n-2,1,-1): 
        if arr[i]!=x: 
            curr = arr[i] 
            arr[i] = prev 
            prev = curr 

    # If element was not found  
    if i<0: 
        return 0

    # Else move the next element in place of x  
    arr[i] = prev 
    return n-1

# Driver code 
arr = [11,15,6,8,9,10] 
n = len(arr) 
x = 6
n = deleteElement(arr,n,x) 
print("Modified array is") 
for i in range(n): 
    print(arr[i],end=" ") 

# This code is contributed by Shrikant13 

```

## C#

```cs

// C# program to remove a given 
// element from an array 
using System; 
class GFG { 

    // This function removes an 
    // element x from arr[] and 
    // returns new size after  
    // removal. Returned size is 
    // n-1 when element is present. 
    // Otherwise 0 is returned to  
    // indicate failure. 
    static int deleteElement(int []arr,  
                             int n,  
                             int x) 
    { 

        // If x is last element, 
        // nothing to do 
        if (arr[n - 1] == x) 
            return (n - 1); 

        // Start from rightmost  
        // element and keep moving 
        // elements one position ahead. 
        int prev = arr[n - 1], i; 
        for (i = n - 2; i >= 0 && 
                arr[i] != x; i--) 
        { 
            int curr = arr[i]; 
            arr[i] = prev; 
            prev = curr; 
        } 

        // If element was  
        // not found 
        if (i < 0) 
            return 0; 

        // Else move the next  
        // element in place of x 
        arr[i] = prev; 

        return (n - 1); 
    } 

    // Driver Code  
    public static void Main() 
    { 
        int []arr = {11, 15, 6, 8, 9, 10}; 
        int n = arr.Length; 
        int x = 6; 

        // Delete x from arr[] 
        n = deleteElement(arr, n, x); 

        Console.WriteLine("Modified array is"); 
        for(int i = 0; i < n; i++) 
            Console.Write(arr[i]+" "); 

    } 
} 

// This code is contributed by anuj_67\. 

```

**输出**：

```
Modified array is
11 15 8 9 10
```

即使给定要删除元素的索引，从数组中删除元素也需要`O(n)`时间。 对于排序数组，时间复杂度也保持为`O(n)`。

在链表中，如果我们知道指向要删除的节点的上一个节点的指针，则可以在`O(1)`时间进行删除。

