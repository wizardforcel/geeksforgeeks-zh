# 间隔之和以及带有除数的更新

> 原文： [https://www.geeksforgeeks.org/sum-interval-update-number-divisors/](https://www.geeksforgeeks.org/sum-interval-update-number-divisors/)

给定一个由`N`个整数组成的数组`A`。 您必须回答两种查询：

1\. 更新`[l, r]` – 对于从`l`到`r`范围内的每个`i`，用`D(A[i])`来更新`A[i]`，其中`D(A[i])`表示`A[i]`的除数的数量。

2\. 查询`[l, r]` – 计算范围在`l`和之间的所有数字的总和。

输入为两个整数`N`和`Q`，分别表示数组中的整数数和查询数。 下一行包含`n`个整数数组，后跟`Q`个查询，其中第一个查询表示为`type[i]`，`l[i]`，`r[i]`。

**先决条件**：[二叉索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/) | [段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)

例子 ：

```
Input : 7 4
        6 4 1 10 3 2 4
        2 1 7
        2 4 5
        1 3 5
        2 4 4
Output : 30
         13
         4

```

**说明**：第一个查询是计算从`A[1]`到`A[7`的数字总和，即`6 + 4 + 1 + 10 + 3 + 2 + 4 =30`。类似，第二个查询结果为 13。对于第三个查询，是更新操作，因此`A[3]`将保持为 1，`A[4]`将变为 4。`A[5]`将变为 2。第四个查询将得出`A[4] = 4`。



**朴素的方法**：

一个简单的解决方案是运行一个从`l`到`r`的循环，并计算给定范围内的元素之和。 要更新值，请预先计算每个数字的除数的值，然后简单地做`arri] = divisors[arr[i]]`。

**高效方法**：

的想法是减少每个查询的时间复杂度，并将操作更新为`O(logN)`。 使用二叉索引树（BIT）或段树。 构造一个`BIT[]`数组，并具有两个用于查询和更新操作的函数，并针对每个数字预先计算除数的数量。 现在，对于每个更新操作，主要观察到的是数字 1 和 2 的除数分别为 1 和 2，因此，如果它存在于更新查询的范围内，则它们不存在。 不需要更新。 我们将使用一个集合来存储仅大于 2 的那些数字的索引，并使用二分搜索来查找更新查询的`l`索引并递增`l`索引，直到在该更新查询的范围内每个元素都被更新为止。 如果`arr[i]`只有 2 个除数，则在更新后将其从集合中删除，因为即使在下一次更新查询之后它也始终为 2。 对于总和查询操作，只需执行`query(r) – query(l – 1)`。

```

// CPP program to calculate sum  
// in an interval and update with 
// number of divisors 
#include <bits/stdc++.h> 
using namespace std; 

int divisors[100], BIT[100]; 

// structure for queries with members type,  
// leftIndex, rightIndex of the query 
struct queries 
{ 
    int type, l, r; 
}; 

// function to calculate the number  
// of divisors of each number 
void calcDivisors() 
{ 
    for (int i = 1; i < 100; i++) { 
        for (int j = i; j < 100; j += i) { 
            divisors[j]++;  
        } 
    } 
} 

// function for updating the value 
void update(int x, int val, int n) 
{ 
    for (x; x <= n; x += x&-x) { 
        BIT[x] += val; 
    } 
} 

// function for calculating the required  
// sum between two indexes 
int sum(int x) 
{ 
    int s = 0; 
    for (x; x > 0; x -= x&-x) { 
        s += BIT[x];  
    } 
    return s; 
} 

// function to return answer to queries 
void answerQueries(int arr[], queries que[], int n, int q) 
{ 
    // Declaring a Set 
    set<int> s; 
    for (int i = 1; i < n; i++) { 

        // inserting indexes of those numbers  
        // which are greater than 2 
        if(arr[i] > 2) s.insert(i); 
        update(i, arr[i], n); 
    } 

    for (int i = 0; i < q; i++) { 

        // update query 
        if (que[i].type == 1) {  
            while (true) { 

                // find the left index of query in  
                // the set using binary search 
                auto it = s.lower_bound(que[i].l); 

                // if it crosses the right index of  
                // query or end of set, then break 
                if(it == s.end() || *it > que[i].r) break; 

                que[i].l = *it; 

                // update the value of arr[i] to  
                // its number of divisors 
                update(*it, divisors[arr[*it]] - arr[*it], n); 

                arr[*it] = divisors[arr[*it]]; 

                // if updated value becomes less than or  
                // equal to 2 remove it from the set 
                if(arr[*it] <= 2) s.erase(*it); 

                // increment the index 
                que[i].l++; 
            } 
        } 

        // sum query 
        else { 
            cout << (sum(que[i].r) - sum(que[i].l - 1)) << endl; 
        } 
    } 
} 

// Driver Code 
int main()  
{ 
    // precompute the number of divisors for each number 
    calcDivisors();  

    int q = 4; 

    // input array 
    int arr[] = {0, 6, 4, 1, 10, 3, 2, 4}; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    // declaring array of structure of type queries 
    queries que[q + 1];  

    que[0].type = 2, que[0].l = 1, que[0].r = 7; 
    que[1].type = 2, que[1].l = 4, que[1].r = 5; 
    que[2].type = 1, que[2].l = 3, que[2].r = 5; 
    que[3].type = 2, que[3].l = 4, que[3].r = 4; 

    // answer the Queries 
    answerQueries(arr, que, n, q); 

    return 0; 
} 

```

**输出**：

```
30
13
4

```

**回答`Q`查询的时间复杂度为`O(Q * log(N))`。**



* * *

* * *



