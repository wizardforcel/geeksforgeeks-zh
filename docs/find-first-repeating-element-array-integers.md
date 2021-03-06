# 在整数数组中找到第一个重复元素

> 原文： [https://www.geeksforgeeks.org/find-first-repeating-element-array-integers/](https://www.geeksforgeeks.org/find-first-repeating-element-array-integers/)

给定一个整数数组，在其中找到第一个重复元素。 我们需要找到多次出现并且第一次出现的索引最小的元素。

**示例**：

```
Input:  arr[] = {10, 5, 3, 4, 3, 5, 6}
Output: 5 [5 is the first element that repeats]

Input:  arr[] = {6, 10, 5, 4, 9, 120, 4, 6, 10}
Output: 6 [6 is the first element that repeats]

```



**简单解决方案**是使用两个嵌套循环。 外循环一个接一个地选择一个元素，内循环检查该元素是否重复。 找到重复的元素后，我们将中断循环并打印该元素。 该解决方案的时间复杂度为`O(n^2)`。

我们可以**使用排序**解决`O(nLogn)`时间的问题。 以下是详细步骤。

1.  将给定数组复制到辅助数组`temp[]`。

2.  使用`O(nLogn)`时间排序算法对临时数组进行排序。

3.  从左到右扫描输入数组。 对于每个元素，[使用二分搜索](https://www.geeksforgeeks.org/count-number-of-occurrences-in-a-sorted-array/)在`temp[]`中计算其出现次数。 一旦发现一个元素出现多次，我们将返回该元素。 此步骤可以在`O(nLogn)`时间完成。

我们可以使用[**散列**](http://geeksquiz.com/hashing-set-1-introduction/)来平均解决`O(n)`时间。 这个想法是从右到左遍历给定的数组，并在我们找到在右侧访问过的元素时更新最小索引。 感谢 Mohammad Shahid 提出了此解决方案。

以下是此想法的实现。

## C++ 

```cpp

/* C++ program to find first repeating element in arr[] */
#include<bits/stdc++.h> 
using namespace std; 

// This function prints the first repeating element in arr[] 
void printFirstRepeating(int arr[], int n) 
{ 
    // Initialize index of first repeating element 
    int min = -1; 

    // Creates an empty hashset 
    set<int> myset; 

    // Traverse the input array from right to left 
    for (int i = n - 1; i >= 0; i--) 
    { 
        // If element is already in hash set, update min 
        if (myset.find(arr[i]) != myset.end()) 
            min = i; 

        else   // Else add element to hash set 
            myset.insert(arr[i]); 
    } 

    // Print the result 
    if (min != -1) 
        cout << "The first repeating element is " << arr[min]; 
    else
        cout << "There are no repeating elements"; 
} 

// Driver method to test above method 
int main() 
{ 
    int arr[] = {10, 5, 3, 4, 3, 5, 6}; 

    int n = sizeof(arr) / sizeof(arr[0]); 
    printFirstRepeating(arr, n); 
} 
//This article is contributed by Chhavi 

```

## Java

```java

/* Java program to find first repeating element in arr[] */
import java.util.*; 

class Main 
{ 
    // This function prints the first repeating element in arr[] 
    static void printFirstRepeating(int arr[]) 
    { 
        // Initialize index of first repeating element 
        int min = -1; 

        // Creates an empty hashset 
        HashSet<Integer> set = new HashSet<>(); 

        // Traverse the input array from right to left 
        for (int i=arr.length-1; i>=0; i--) 
        { 
            // If element is already in hash set, update min 
            if (set.contains(arr[i])) 
                min = i; 

            else   // Else add element to hash set 
                set.add(arr[i]); 
        } 

        // Print the result 
        if (min != -1) 
          System.out.println("The first repeating element is " + arr[min]); 
        else
          System.out.println("There are no repeating elements"); 
    } 

    // Driver method to test above method 
    public static void main (String[] args) throws java.lang.Exception 
    { 
        int arr[] = {10, 5, 3, 4, 3, 5, 6}; 
        printFirstRepeating(arr); 
    } 
} 

```

## Python3

```py

# Python3 program to find first repeating 
# element in arr[]  

# This function prints the first repeating  
# element in arr[] 
def printFirstRepeating(arr, n): 

    # Initialize index of first repeating element 
    Min = -1

    # Creates an empty hashset 
    myset = dict() 

    # Traverse the input array from right to left 
    for i in range(n - 1, -1, -1): 

        # If element is already in hash set, 
        # update Min 
        if arr[i] in myset.keys(): 
            Min = i 

        else: # Else add element to hash set 
            myset[arr[i]] = 1

    # Print the result 
    if (Min != -1): 
        print("The first repeating element is",  
                                      arr[Min]) 
    else: 
        print("There are no repeating elements") 

# Driver Code 
arr = [10, 5, 3, 4, 3, 5, 6] 

n = len(arr) 
printFirstRepeating(arr, n) 

# This code is contributed by Mohit kumar 29 

```

## C# 

```cs

using System; 
using System.Collections.Generic; 

/* C# program to find first repeating element in arr[] */

public class GFG 
{ 
    // This function prints the first repeating element in arr[]  
    public static void printFirstRepeating(int[] arr) 
    { 
        // Initialize index of first repeating element  
        int min = -1; 

        // Creates an empty hashset  
        HashSet<int> set = new HashSet<int>(); 

        // Traverse the input array from right to left  
        for (int i = arr.Length - 1; i >= 0; i--) 
        { 
            // If element is already in hash set, update min  
            if (set.Contains(arr[i])) 
            { 
                min = i; 
            } 

            else // Else add element to hash set 
            { 
                set.Add(arr[i]); 
            } 
        } 

        // Print the result  
        if (min != -1) 
        { 
          Console.WriteLine("The first repeating element is " + arr[min]); 
        } 
        else
        { 
          Console.WriteLine("There are no repeating elements"); 
        } 
    } 

    // Driver method to test above method  

    public static void Main(string[] args) 
    { 
        int[] arr = new int[] {10, 5, 3, 4, 3, 5, 6}; 
        printFirstRepeating(arr); 
    } 
} 

// This code is contributed by Shrikant13 

```

输出：

```
The first repeating element is 5
```

