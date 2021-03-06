# 在 C++ STL 中的按值对映射排序

> 原文：[https://www.geeksforgeeks.org/sorting-a-map-by-value-in-c-stl/](https://www.geeksforgeeks.org/sorting-a-map-by-value-in-c-stl/)

[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)是以映射方式存储元素的关联容器。 每个元素都有一个键值和一个映射值。 任何两个映射值都不能具有相等的键值。 默认情况下， [C++](http://www.geeksforgeeks.org/c-plus-plus/) 中的`Map`根据其键以升序排序。 下面是实现此目的的各种方法：

**方法 1 - 使用[偶对向量](http://www.geeksforgeeks.org/vector-in-cpp-stl/)**：想法是将映射中的所有内容复制到[对应向量中](https://www.geeksforgeeks.org/pair-in-cpp-stl/)和[使用下面给出的](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/) [lambda 函数](https://www.geeksforgeeks.org/lambda-expression-in-c/)根据第二值对对向量排序：

```
bool cmp(pair<T1, T2>& a,
         pair<T1, T2>& b)
{
    return a.second < b.second;
}

where T1 and T2
are the data-types 
that can be the 
same or different.

```

下面是上述方法的实现：

```cpp
// C++ program for the above approach 
  
#include <bits/stdc++.h> 
using namespace std; 
  
// Comparator function to sort pairs 
// according to second value 
bool cmp(pair<string, int>& a, 
         pair<string, int>& b) 
{ 
    return a.second < b.second; 
} 
  
// Function to sort the map according 
// to value in a (key-value) pairs 
void sort(map<string, int>& M) 
{ 
  
    // Declare vector of pairs 
    vector<pair<string, int> > A; 
  
    // Copy key-value pair from Map 
    // to vector of pairs 
    for (auto& it : M) { 
        A.push_back(it); 
    } 
  
    // Sort using comparator function 
    sort(A.begin(), A.end(), cmp); 
  
    // Print the sorted value 
    for (auto& it : A) { 
  
        cout << it.first << ' '
             << it.second << endl; 
    } 
} 
  
// Driver Code 
int main() 
{ 
  
    // Declare Map 
    map<string, int> M; 
  
    // Given Map 
    M = { { "GfG", 3 }, 
          { "To", 2 }, 
          { "Welcome", 1 } }; 
  
    // Function Call 
    sort(M); 
    return 0; 
} 
```

**输出**：

```
Welcome 1
To 2
GfG 3

```

**方法 2 – 使用偶对集合**：想法是将映射中的所有（键值）对插入可以使用比较器函数构造的偶对集合中，根据第二个值对偶对排序。

下面是上述方法的实现：

```cpp
// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 
  
// Comparison function for sorting the 
// set by increasing order of its pair's 
// second value 
struct comp { 
    template <typename T> 
  
    // Comparator function 
    bool operator()(const T& l, 
                    const T& r) const
    { 
        if (l.second != r.second) { 
            return l.second < r.second; 
        } 
        return l.first < r.first; 
    } 
}; 
  
// Function to sort the map according 
// to value in a (key-value) pairs 
void sort(map<string, int>& M) 
{ 
  
    // Declare set of pairs and insert 
    // pairs according to the comparator 
    // function comp() 
    set<pair<string, int>, comp> S(M.begin(), 
                                   M.end()); 
  
    // Print the sorted value 
    for (auto& it : S) { 
        cout << it.first << ' '
             << it.second << endl; 
    } 
} 
  
// Driver Code 
int main() 
{ 
  
    // Declare Map 
    map<string, int> M; 
  
    // Given Map 
    M = { { "GfG", 3 }, 
          { "To", 2 }, 
          { "Welcome", 1 } }; 
  
    // Function Call 
    sort(M); 
    return 0; 
} 
```

**输出**：

```
Welcome 1
To 2
GfG 3

```

**方法 3 – 使用[多重映射](https://www.geeksforgeeks.org/multimap-associative-containers-the-c-standard-template-library-stl/)**

多重映射类似于映射，不同之处在于多个元素可以具有相同的键。 在这种情况下，键值和映射值对必须是唯一的，而不是每个元素都是唯一的。

的想法是使用原始映射的值作为多映射中的键，并将原始映射的键值作为多映射中的值，将给定映射中的所有对插入多映射中。

下面是上述方法的实现：

```cpp
// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 
  
// Function to sort the map according 
// to value in a (key-value) pairs 
void sort(map<string, int>& M) 
{ 
  
    // Declare a multimap 
    multimap<int, string> MM; 
  
    // Insert every (key-value) pairs from 
    // map M to multimap MM as (value-key) 
    // pairs 
    for (auto& it : M) { 
        MM.insert({ it.second, it.first }); 
    } 
  
    // Print the multimap 
    for (auto& it : MM) { 
        cout << it.second << ' '
             << it.first << endl; 
    } 
} 
  
// Driver Code 
int main() 
{ 
  
    // Declare Map 
    map<string, int> M; 
  
    // Given Map 
    M = { { "GfG", 3 }, 
          { "To", 2 }, 
          { "Welcome", 1 } }; 
  
    // Function Call 
    sort(M); 
    return 0; 
} 
```

**输出**：

```
Welcome 1
To 2
GfG 3

```



* * *

* * *



