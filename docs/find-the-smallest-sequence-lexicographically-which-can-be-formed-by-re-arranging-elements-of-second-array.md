# 查找词典上最小的序列，可以通过重新排列第二个数组的元素生成

> 原文：[https://www.geeksforgeeks.org/find-the-smallest-sequence-lexicographically-which-can-be-formed-by-re-arranging-elements-of-second-array/](https://www.geeksforgeeks.org/find-the-smallest-sequence-lexicographically-which-can-be-formed-by-re-arranging-elements-of-second-array/)


给定`N`个整数的两个数组`A`和`B`。 重新排列`B`元素本身的方式，使重新排列后`(A[i] + B[i]) % N`生成的序列在字典上最小。 该任务是按字典顺序打印**最小的**序列。

**注意**：数组元素在`[0, n)`范围内。

**示例**：

> **输入**：`a[] = {0, 1, 2, 1}, b[] = {3, 2, 1, 1}`
>
> **输出**：`1 0 0 2`
>
> 将`B`重新排序为`{1, 3, 2, 1}`，以获得可能的最小序列。
> 
> **输入**：`a[] = {2, 0, 0}, b[] = {1, 0, 2}`
>
> **输出**：`0 0 2`

**方法**：可以贪婪地解决问题。 最初使用哈希保留所有数组`B`的数目的计数，并将它们存储在 C++ 中[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中，以便使用[`lower_bound()`](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/)来检查元素和[`delete()`](https://www.geeksforgeeks.org/multiset-erase-in-c-stl/)来删除元素，可以在对数时间内进行操作。

对于数组中的每个元素，请使用`lower_bound`函数检查是否等于或大于`n - a [i]`的数字。 如果没有这样的元素，则采用集合中最小的元素。 将哈希表中使用的数字减少 1，如果哈希表的值为 0，则还将集合中的元素也删除。

但是，如果数组元素为 0，则存在例外，然后首先检查 0，然后检查`N`，如果两个都不存在，则取最小的元素。

下面是上述方法的实现：

```cpp
// C++ implementation of the 
// above approach 
  
#include <bits/stdc++.h> 
using namespace std; 
  
// Function to get the smallest 
// sequence possible 
void solve(int a[], int b[], int n) 
{ 
  
    // Hash-table to count the 
    // number of occurrences of b[i] 
    unordered_map<int, int> mpp; 
  
    // Store the element in sorted order 
    // for using binary search 
    set<int> st; 
  
    // Iterate in the B array 
    // and count the occurrences and 
    // store in the set 
    for (int i = 0; i < n; i++) { 
        mpp[b[i]]++; 
        st.insert(b[i]); 
    } 
  
    vector<int> sequence; 
  
    // Iterate for N elements 
    for (int i = 0; i < n; i++) { 
  
        // If the element is 0 
        if (a[i] == 0) { 
  
            // Find the nearest number to 0 
            auto it = st.lower_bound(0); 
            int el = *it; 
            sequence.push_back(el % n); 
  
            // Decrease the count 
            mpp[el]--; 
  
            // Erase if no more are there 
            if (!mpp[el]) 
                st.erase(el); 
        } 
  
        // If the element is other than 0 
        else { 
  
            // Find the difference 
            int x = n - a[i]; 
  
            // Find the nearest number which can give us 
            // 0 on modulo 
            auto it = st.lower_bound(x); 
  
            // If no such number occurs then 
            // find the number closest to 0 
            if (it == st.end()) 
                it = st.lower_bound(0); 
  
            // Get the number 
            int el = *it; 
  
            // store the number 
            sequence.push_back((a[i] + el) % n); 
  
            // Decrease the count 
            mpp[el]--; 
  
            // If no more appers, then erase it from set 
            if (!mpp[el]) 
                st.erase(el); 
        } 
    } 
  
    for (auto it : sequence) 
        cout << it << " "; 
} 
  
// Driver Code 
int main() 
{ 
    int a[] = { 0, 1, 2, 1 }; 
    int b[] = { 3, 2, 1, 1 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    solve(a, b, n); 
    return 0; 
} 
```

**输出**：

```
1 0 0 2

```



* * *

* * *



