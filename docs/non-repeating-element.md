# 非重复元素

> 原文： [https://www.geeksforgeeks.org/non-repeating-element/](https://www.geeksforgeeks.org/non-repeating-element/)

在给定的整数数组中找到第一个非重复元素。

**示例**：

```
Input : -1 2 -1 3 2
Output : 3
Explanation : The first number that does not 
repeat is : 3

Input : 9 4 9 6 7 4
Output : 6

```



**简单解决方案**是使用两个循环。 外循环一个接一个地挑选元素，内循环检查该元素是否存在一次以上。

## C++ 

```cpp

// Simple CPP program to find first non- 
// repeating element. 
#include <bits/stdc++.h> 
using namespace std; 

int firstNonRepeating(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) { 
        int j; 
        for (j = 0; j < n; j++) 
            if (i != j && arr[i] == arr[j]) 
                break; 
        if (j == n) 
            return arr[i]; 
    } 
    return -1; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 9, 4, 9, 6, 7, 4 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << firstNonRepeating(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find first non-repeating 
// element. 
class GFG { 

    static int firstNonRepeating(int arr[], int n) 
    { 
        for (int i = 0; i < n; i++) { 
            int j; 
            for (j = 0; j < n; j++) 
                if (i != j && arr[i] == arr[j]) 
                    break; 
            if (j == n) 
                return arr[i]; 
        } 

        return -1; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 

        int arr[] = { 9, 4, 9, 6, 7, 4 }; 
        int n = arr.length; 

        System.out.print(firstNonRepeating(arr, n)); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python3 program to find first  
# non-repeating element. 

def firstNonRepeating(arr, n): 

    for i in range(n): 
        j = 0
        while(j < n): 
            if (i != j and arr[i] == arr[j]): 
                break
            j += 1
        if (j == n): 
            return arr[i] 

    return -1

# Driver code 
arr = [ 9, 4, 9, 6, 7, 4 ] 
n = len(arr) 
print(firstNonRepeating(arr, n)) 

# This code is contributed by Anant Agarwal. 

```

## C# 

```cs

// C# program to find first non- 
// repeating element. 
using System; 

class GFG { 
    static int firstNonRepeating(int[] arr, int n) 
    { 
        for (int i = 0; i < n; i++) { 
            int j; 
            for (j = 0; j < n; j++) 
                if (i != j && arr[i] == arr[j]) 
                    break; 
            if (j == n) 
                return arr[i]; 
        } 
        return -1; 
    } 

    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 9, 4, 9, 6, 7, 4 }; 
        int n = arr.Length; 
        Console.Write(firstNonRepeating(arr, n)); 
    } 
} 
// This code is contributed by Anant Agarwal. 

```

## PHP

```php

<?php 
// Simple PHP program to find first non- 
// repeating element. 

function firstNonRepeating($arr, $n) 
{ 
    for ($i = 0; $i < $n; $i++) 
    { 
        $j; 
        for ($j = 0; $j< $n; $j++) 
            if ($i != $j && $arr[$i] == $arr[$j]) 
                break; 
        if ($j == $n) 
            return $arr[$i]; 
    } 
    return -1; 
} 

    // Driver code 
    $arr = array(9, 4, 9, 6, 7, 4); 
    $n = sizeof($arr) ; 
    echo firstNonRepeating($arr, $n); 

// This code is contributed by ajit 
?> 

```

**输出**：

```
6

```

**有效解决方案**将使用哈希。

1.  遍历数组，在哈希表中插入元素及其计数。

2.  再次遍历数组，并打印计数等于 1 的第一个元素。

## C++

```cpp

// Efficient CPP program to find first non- 
// repeating element. 
#include <bits/stdc++.h> 
using namespace std; 

int firstNonRepeating(int arr[], int n) 
{ 
    // Insert all array elements in hash 
    // table 
    unordered_map<int, int> mp; 
    for (int i = 0; i < n; i++) 
        mp[arr[i]]++; 

    // Traverse array again and return 
    // first element with count 1\. 
    for (int i = 0; i < n; i++) 
        if (mp[arr[i]] == 1) 
            return arr[i]; 
    return -1; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 9, 4, 9, 6, 7, 4 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << firstNonRepeating(arr, n); 
    return 0; 
} 

```

## Java

```java

// Efficient Java program to find first non- 
// repeating element. 
import java.util.*; 

class GFG { 

    static int firstNonRepeating(int arr[], int n) 
    { 
        // Insert all array elements in hash 
        // table 

        Map<Integer, Integer> m = new HashMap<>(); 
        for (int i = 0; i < n; i++) { 
            if (m.containsKey(arr[i])) { 
                m.put(arr[i], m.get(arr[i]) + 1); 
            } 
            else { 
                m.put(arr[i], 1); 
            } 
        } 
        // Traverse array again and return 
        // first element with count 1\. 
        for (int i = 0; i < n; i++) 
            if (m.get(arr[i]) == 1) 
                return arr[i]; 
        return -1; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 9, 4, 9, 6, 7, 4 }; 
        int n = arr.length; 
        System.out.println(firstNonRepeating(arr, n)); 
    } 
} 

// This code contributed by Rajput-Ji 

```

## Python3

```py

# Efficient Python3 program to find first  
# non-repeating element. 
from collections import defaultdict 

def firstNonRepeating(arr, n): 
    mp = defaultdict(lambda:0) 

    # Insert all array elements in hash table  
    for i in range(n): 
        mp[arr[i]] += 1

    # Traverse array again and return  
    # first element with count 1.  
    for i in range(n): 
        if mp[arr[i]] == 1: 
            return arr[i] 
    return -1

# Driver Code 
arr = [9, 4, 9, 6, 7, 4] 
n = len(arr) 
print(firstNonRepeating(arr, n))  

# This code is contributed by Shrikant13 

```

## C#

```cs

// Efficient C# program to find first non- 
// repeating element. 
using System; 
using System.Collections.Generic; 

class GFG { 

    static int firstNonRepeating(int[] arr, int n) 
    { 
        // Insert all array elements in hash 
        // table 

        Dictionary<int, int> m = new Dictionary<int, int>(); 
        for (int i = 0; i < n; i++) { 
            if (m.ContainsKey(arr[i])) { 
                var val = m[arr[i]]; 
                m.Remove(arr[i]); 
                m.Add(arr[i], val + 1); 
            } 
            else { 
                m.Add(arr[i], 1); 
            } 
        } 

        // Traverse array again and return 
        // first element with count 1\. 
        for (int i = 0; i < n; i++) 
            if (m[arr[i]] == 1) 
                return arr[i]; 
        return -1; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        int[] arr = { 9, 4, 9, 6, 7, 4 }; 
        int n = arr.Length; 
        Console.WriteLine(firstNonRepeating(arr, n)); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
6

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。

**进一步优化**：如果数组有很多重复项，我们还可以使用哈希表（其中值是[偶对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)），将索引存储在哈希表中。 现在，我们只需要遍历哈希表中的键（不是完整的数组）即可找到第一个非重复的键。

**打印所有非重复元素**：

## C++

```cpp

// Efficient CPP program to print all non- 
// repeating elements. 
#include <bits/stdc++.h> 
using namespace std; 

void firstNonRepeating(int arr[], int n) 
{ 
    // Insert all array elements in hash 
    // table 
    unordered_map<int, int> mp; 
    for (int i = 0; i < n; i++) 
        mp[arr[i]]++; 

    // Traverse through map only and 
    for (auto x : mp) 
        if (x.second == 1) 
            cout << x.first << " "; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 9, 4, 9, 6, 7, 4 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    firstNonRepeating(arr, n); 
    return 0; 
} 

```

## Java

```java

// Efficient Java program to print all non- 
// repeating elements. 
import java.util.*; 

class GFG { 

    static void firstNonRepeating(int arr[], int n) 
    { 
        // Insert all array elements in hash 
        // table 
        Map<Integer, Integer> m = new HashMap<>(); 
        for (int i = 0; i < n; i++) { 
            if (m.containsKey(arr[i])) { 
                m.put(arr[i], m.get(arr[i]) + 1); 
            } 
            else { 
                m.put(arr[i], 1); 
            } 
        } 

        // Traverse through map only and 
        // using for-each loop for iteration over Map.entrySet() 
        for (Map.Entry<Integer, Integer> x : m.entrySet()) 
            if (x.getValue() == 1) 
                System.out.print(x.getKey() + " "); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 9, 4, 9, 6, 7, 4 }; 
        int n = arr.length; 
        firstNonRepeating(arr, n); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

## Python3

```py

# Efficient Python program to print all non- 
# repeating elements. 

def firstNonRepeating(arr, n): 

    # Insert all array elements in hash 
    # table 
    mp={} 
    for i in range(n): 
        if arr[i] not in mp: 
            mp[arr[i]]=0
        mp[arr[i]]+=1

    # Traverse through map only and 
    for x in mp: 
        if (mp[x]== 1): 
            print(x,end=" ") 

# Driver code 
arr = [ 9, 4, 9, 6, 7, 4 ] 
n = len(arr) 
firstNonRepeating(arr, n) 

# This code is contributed by shivanisinghss2110 

```

## C#

```cs

// Efficient C# program to print all non- 
// repeating elements. 
using System; 
using System.Collections.Generic; 

class GFG { 

    static void firstNonRepeating(int[] arr, int n) 
    { 
        // Insert all array elements in hash 
        // table 
        Dictionary<int, int> m = new Dictionary<int, int>(); 
        for (int i = 0; i < n; i++) { 
            if (m.ContainsKey(arr[i])) { 
                var val = m[arr[i]]; 
                m.Remove(arr[i]); 
                m.Add(arr[i], val + 1); 
            } 
            else { 
                m.Add(arr[i], 1); 
            } 
        } 

        // Traverse through map only and 
        // using for-each loop for iteration over Map.entrySet() 
        foreach(KeyValuePair<int, int> x in m) 
        { 
            if (x.Value == 1) { 
                Console.Write(x.Key + " "); 
            } 
        } 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        int[] arr = { 9, 4, 9, 6, 7, 4 }; 
        int n = arr.Length; 
        firstNonRepeating(arr, n); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
7 6

```



* * *

* * *



