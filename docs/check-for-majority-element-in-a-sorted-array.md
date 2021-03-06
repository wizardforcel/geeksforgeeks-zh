# 检查排序数组中的多数元素

> 原文： [https://www.geeksforgeeks.org/check-for-majority-element-in-a-sorted-array/](https://www.geeksforgeeks.org/check-for-majority-element-in-a-sorted-array/)

**问题**：编写一个 C 函数，以查找给定的整数`x`在`n`个整数的排序数组中是否出现`n / 2`次以上。

基本上，我们需要编写一个名为`isMajority()`的函数，该函数将数组（`arr[]`），数组的大小（`n`）和要搜索的数字（`x`）作为参数，并且如果`x`是[多数元素](https://www.geeksforgeeks.org/majority-element/)（出现次数超过`n / 2`次），则返回`true`。

例子：

```
Input: arr[] = {1, 2, 3, 3, 3, 3, 10}, x = 3
Output: True (x appears more than n/2 times in the given array)

Input: arr[] = {1, 1, 2, 4, 4, 4, 6, 6}, x = 4
Output: False (x doesn't appear more than n/2 times in the given array)

Input: arr[] = {1, 1, 1, 2, 2}, x = 1
Output: True (x appears more than n/2 times in the given array)

```



**方法 1（使用线性搜索）**：

线性搜索元素的第一个匹配项，找到它后（在索引`i`处放置），在索引`i + n / 2`处检查元素。 如果元素存在于`i + n / 2`，则返回 1，否则返回 0。

## C

```c

/* C Program to check for majority element in a sorted array */
# include <stdio.h> 
# include <stdbool.h> 

bool isMajority(int arr[], int n, int x) 
{ 
    int i; 

    /* get last index according to n (even or odd) */
    int last_index = n%2? (n/2+1): (n/2); 

    /* search for first occurrence of x in arr[]*/
    for (i = 0; i < last_index; i++) 
    { 
        /* check if x is present and is present more than n/2 
           times */
        if (arr[i] == x && arr[i+n/2] == x) 
            return 1; 
    } 
    return 0; 
} 

/* Driver program to check above function */
int main() 
{ 
     int arr[] ={1, 2, 3, 4, 4, 4, 4}; 
     int n = sizeof(arr)/sizeof(arr[0]); 
     int x = 4; 
     if (isMajority(arr, n, x)) 
        printf("%d appears more than %d times in arr[]", 
               x, n/2); 
     else
        printf("%d does not appear more than %d times in arr[]", 
                x, n/2); 

   return 0; 
} 

```

## Java

```java

/* Program to check for majority element in a sorted array */
import java.io.*; 

class Majority { 

    static boolean isMajority(int arr[], int n, int x) 
    { 
        int i, last_index = 0; 

        /* get last index according to n (even or odd) */
        last_index = (n%2==0)? n/2: n/2+1; 

        /* search for first occurrence of x in arr[]*/
        for (i = 0; i < last_index; i++) 
        { 
            /* check if x is present and is present more 
               than n/2 times */
            if (arr[i] == x && arr[i+n/2] == x) 
                return true; 
        } 
        return false; 
    } 

    /* Driver function to check for above functions*/
    public static void main (String[] args) { 
        int arr[] = {1, 2, 3, 4, 4, 4, 4}; 
        int n = arr.length; 
        int x = 4; 
        if (isMajority(arr, n, x)==true) 
           System.out.println(x+" appears more than "+ 
                              n/2+" times in arr[]"); 
        else
           System.out.println(x+" does not appear more than "+ 
                              n/2+" times in arr[]"); 
    } 
} 
/*This article is contributed by Devesh Agrawal*/

```

## Python

```py

'''Python3 Program to check for majority element in a sorted array'''

def isMajority(arr, n, x): 
    # get last index according to n (even or odd) */ 
    last_index = (n//2 + 1) if n % 2 == 0 else (n//2) 

    # search for first occurrence of x in arr[]*/ 
    for i in range(last_index): 
        # check if x is present and is present more than n / 2 times */ 
        if arr[i] == x and arr[i + n//2] == x: 
            return 1

# Driver program to check above function */ 
arr = [1, 2, 3, 4, 4, 4, 4] 
n = len(arr) 
x = 4
if (isMajority(arr, n, x)): 
    print ("% d appears more than % d times in arr[]"
                                            %(x, n//2)) 
else: 
    print ("% d does not appear more than % d times in arr[]"
                                                    %(x, n//2)) 

# This code is contributed by shreyanshi_arun. 

```

## C# 

```cs

// C# Program to check for majority 
// element in a sorted array  
using System; 

class GFG { 
    static bool isMajority(int[] arr,  
                            int n, int x) 
    { 
        int i, last_index = 0; 

        // Get last index according to 
        // n (even or odd)  
        last_index = (n % 2 == 0) ? n / 2 : 
                                    n / 2 + 1; 

        // Search for first occurrence  
        // of x in arr[] 
        for (i = 0; i < last_index; i++) { 
            // Check if x is present and  
            // is present more than n/2 times  
            if (arr[i] == x && arr[i + n / 2] == x) 
                return true; 
        } 
        return false; 
    } 

    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 1, 2, 3, 4, 4, 4, 4 }; 
        int n = arr.Length; 
        int x = 4; 
        if (isMajority(arr, n, x) == true) 
            Console.Write(x + " appears more than " +  
                            n / 2 + " times in arr[]"); 
        else
            Console.Write(x + " does not appear more than " +  
                             n / 2 + " times in arr[]"); 
    } 
} 

// This code is contributed by Sam007 

```

## PHP

```php

<?php 
// PHP Program to check for  
// majority element in a  
// sorted array  

// function returns majority 
// element in a sorted array  
function isMajority($arr, $n, $x) 
{ 
    $i; 

    // get last index according 
    // to n (even or odd)  
    $last_index = $n % 2? ($n / 2 + 1): ($n / 2); 

    // search for first occurrence 
    // of x in arr[] 
    for ($i = 0; $i < $last_index; $i++) 
    { 

        // check if x is present and  
        // is present more than n/2 
        // times  
        if ($arr[$i] == $x && $arr[$i + $n / 2] == $x) 
            return 1; 
    } 
    return 0; 
} 

    // Driver Code 
    $arr = array(1, 2, 3, 4, 4, 4, 4); 
    $n = sizeof($arr); 
    $x = 4; 
    if (isMajority($arr, $n, $x)) 
        echo $x, " appears more than "
             , floor($n / 2), " times in arr[]"; 

    else
        echo $x, "does not appear more than "
              , floor($n / 2), "times in arr[]"; 

// This code is contributed by Ajit 
?> 

```

Output :

```
4 appears more than 3 times in arr[]
```

**时间复杂度**：`O(n)`。

**方法 2（使用二分搜索）**：

使用二分搜索方法来查找给定数字的第一个匹配项。 二分搜索的标准在这里很重要。

## C

```c

/* Program to check for majority element in a sorted array */
# include <stdio.h> 
# include <stdbool.h> 

/* If x is present in arr[low...high] then returns the index of 
first occurrence of x, otherwise returns -1 */
int _binarySearch(int arr[], int low, int high, int x); 

/* This function returns true if the x is present more than n/2 
times in arr[] of size n */
bool isMajority(int arr[], int n, int x) 
{ 
    /* Find the index of first occurrence of x in arr[] */
    int i = _binarySearch(arr, 0, n-1, x); 

    /* If element is not present at all, return false*/
    if (i == -1) 
        return false; 

    /* check if the element is present more than n/2 times */
    if (((i + n/2) <= (n -1)) && arr[i + n/2] == x) 
        return true; 
    else
        return false; 
} 

/* If x is present in arr[low...high] then returns the index of 
first occurrence of x, otherwise returns -1 */
int _binarySearch(int arr[], int low, int high, int x) 
{ 
    if (high >= low) 
    { 
        int mid = (low + high)/2; /*low + (high - low)/2;*/

        /* Check if arr[mid] is the first occurrence of x. 
            arr[mid] is first occurrence if x is one of the following 
            is true: 
            (i) mid == 0 and arr[mid] == x 
            (ii) arr[mid-1] < x and arr[mid] == x 
        */
        if ( (mid == 0 || x > arr[mid-1]) && (arr[mid] == x) ) 
            return mid; 
        else if (x > arr[mid]) 
            return _binarySearch(arr, (mid + 1), high, x); 
        else
            return _binarySearch(arr, low, (mid -1), x); 
    } 

    return -1; 
} 

/* Driver program to check above functions */
int main() 
{ 
    int arr[] = {1, 2, 3, 3, 3, 3, 10}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int x = 3; 
    if (isMajority(arr, n, x)) 
        printf("%d appears more than %d times in arr[]", 
               x, n/2); 
    else
        printf("%d does not appear more than %d times in arr[]", 
               x, n/2); 
    return 0; 
} 

```

## Java

```java

/* Program to check for majority element in a sorted array */
import java.io.*; 

class Majority { 

    /* If x is present in arr[low...high] then returns the index of 
        first occurrence of x, otherwise returns -1 */
    static int  _binarySearch(int arr[], int low, int high, int x) 
    { 
        if (high >= low) 
        { 
            int mid = (low + high)/2;  /*low + (high - low)/2;*/

            /* Check if arr[mid] is the first occurrence of x. 
                arr[mid] is first occurrence if x is one of the following 
                is true: 
                (i)  mid == 0 and arr[mid] == x 
                (ii) arr[mid-1] < x and arr[mid] == x 
            */
            if ( (mid == 0 || x > arr[mid-1]) && (arr[mid] == x) ) 
                return mid; 
            else if (x > arr[mid]) 
                return _binarySearch(arr, (mid + 1), high, x); 
            else
                return _binarySearch(arr, low, (mid -1), x); 
        } 

        return -1; 
    } 

    /* This function returns true if the x is present more than n/2 
        times in arr[] of size n */
    static boolean isMajority(int arr[], int n, int x) 
    { 
        /* Find the index of first occurrence of x in arr[] */
        int i = _binarySearch(arr, 0, n-1, x); 

        /* If element is not present at all, return false*/
        if (i == -1) 
            return false; 

        /* check if the element is present more than n/2 times */
        if (((i + n/2) <= (n -1)) && arr[i + n/2] == x) 
            return true; 
        else
            return false; 
    } 

    /*Driver function to check for above functions*/
    public static void main (String[] args)  { 

        int arr[] = {1, 2, 3, 3, 3, 3, 10}; 
        int n = arr.length; 
        int x = 3; 
        if (isMajority(arr, n, x)==true) 
            System.out.println(x + " appears more than "+ 
                              n/2 + " times in arr[]"); 
        else
            System.out.println(x + " does not appear more than " + 
                              n/2 + " times in arr[]"); 
    } 
} 
/*This code is contributed by Devesh Agrawal*/

```

## Python

```py

'''Python3 Program to check for majority element in a sorted array'''

# This function returns true if the x is present more than n / 2 
# times in arr[] of size n */ 
def isMajority(arr, n, x): 

    # Find the index of first occurrence of x in arr[] */ 
    i = _binarySearch(arr, 0, n-1, x) 

    # If element is not present at all, return false*/ 
    if i == -1: 
        return False

    # check if the element is present more than n / 2 times */ 
    if ((i + n//2) <= (n -1)) and arr[i + n//2] == x: 
        return True
    else: 
        return False

# If x is present in arr[low...high] then returns the index of 
# first occurrence of x, otherwise returns -1 */ 
def _binarySearch(arr, low, high, x): 
    if high >= low: 
        mid = (low + high)//2 # low + (high - low)//2; 

        ''' Check if arr[mid] is the first occurrence of x. 
            arr[mid] is first occurrence if x is one of the following 
            is true: 
            (i) mid == 0 and arr[mid] == x 
            (ii) arr[mid-1] < x and arr[mid] == x'''

        if (mid == 0 or x > arr[mid-1]) and (arr[mid] == x): 
            return mid 
        elif x > arr[mid]: 
            return _binarySearch(arr, (mid + 1), high, x) 
        else: 
            return _binarySearch(arr, low, (mid -1), x) 
    return -1

# Driver program to check above functions */ 
arr = [1, 2, 3, 3, 3, 3, 10] 
n = len(arr) 
x = 3
if (isMajority(arr, n, x)): 
    print ("% d appears more than % d times in arr[]"
                                            % (x, n//2)) 
else: 
    print ("% d does not appear more than % d times in arr[]"
                                                    % (x, n//2)) 

# This code is contributed by shreyanshi_arun. 

```

## C#

```cs

// C# Program to check for majority 
// element in a sorted array */ 
using System; 

class GFG { 

    // If x is present in arr[low...high] 
    // then returns the index of first 
    // occurrence of x, otherwise returns -1  
    static int _binarySearch(int[] arr, int low, 
                               int high, int x) 
    { 
        if (high >= low) { 
            int mid = (low + high) / 2;  
            //low + (high - low)/2; 

            // Check if arr[mid] is the first  
            // occurrence of x.    arr[mid] is  
            // first occurrence if x is one of  
            // the following is true: 
            // (i) mid == 0 and arr[mid] == x 
            // (ii) arr[mid-1] < x and arr[mid] == x 

            if ((mid == 0 || x > arr[mid - 1]) && 
                                 (arr[mid] == x)) 
                return mid; 
            else if (x > arr[mid]) 
                return _binarySearch(arr, (mid + 1), 
                                           high, x); 
            else
                return _binarySearch(arr, low, 
                                      (mid - 1), x); 
        } 

        return -1; 
    } 

    // This function returns true if the x is 
    // present more than n/2 times in arr[]  
    // of size n  
    static bool isMajority(int[] arr, int n, int x) 
    { 

        // Find the index of first occurrence 
        // of x in arr[]  
        int i = _binarySearch(arr, 0, n - 1, x); 

        // If element is not present at all, 
        // return false 
        if (i == -1) 
            return false; 

        // check if the element is present  
        // more than n/2 times  
        if (((i + n / 2) <= (n - 1)) && 
                                arr[i + n / 2] == x) 
            return true; 
        else
            return false; 
    } 

    //Driver code 
    public static void Main() 
    { 

        int[] arr = { 1, 2, 3, 3, 3, 3, 10 }; 
        int n = arr.Length; 
        int x = 3; 
        if (isMajority(arr, n, x) == true) 
           Console.Write(x + " appears more than " + 
                             n / 2 + " times in arr[]"); 
        else
           Console.Write(x + " does not appear more than " + 
                             n / 2 + " times in arr[]"); 
    } 
} 

// This code is contributed by Sam007 

```

Output:

```
3 appears more than 3 times in arr[]
```

**时间复杂度**：`O(Logn)`。

**算法范例**：分治。

如果您在上述程序/算法中发现任何错误或解决相同问题的更好方法，请写评论。

