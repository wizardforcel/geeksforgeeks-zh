# C++ STL 中的栈列表

> 原文：[https://www.geeksforgeeks.org/list-of-stacks-in-c-stl/](https://www.geeksforgeeks.org/list-of-stacks-in-c-stl/)

**先决条件**：[列表](https://www.geeksforgeeks.org/list-cpp-stl/)，[栈](https://www.geeksforgeeks.org/stack-data-structure/)

**列表**是允许[非连续内存分配](https://www.geeksforgeeks.org/non-contiguous-allocation-in-operating-system/)的序列容器。 与[向量](http://www.geeksforgeeks.org/vector-in-cpp-stl/)相比，列表的遍历速度较慢，但​​是一旦找到位置，插入和删除速度就会很快。

**语法**：

```
list<Type> name_of_list;
```

[**栈**](http://www.geeksforgeeks.org/stack-data-structure/) 是一种容器适配器，具有的 LIFO（后进先出）类型，其中在一端添加新元素，并且仅从该端（顶部）删除元素。

**语法**：

```
stack name_of_stack;
```

**栈列表**是具有一系列栈的容器的类型，这是一个二维容器，其中`N`行的列表和`M`列的栈 ，两个大小的大小都是不固定的。 可以使用[迭代器](https://www.geeksforgeeks.org/iterators-c-stl/) 遍历和访问的。

**语法**：

```
list<stack> name_of_container(size);
```

大小可选。

![](img/613ddcac41d3b7f794d44f0223b1d831.png)

**示例**：

```
list<stack> ls(10);
```

栈列表的大小为 10。

**插入**：[使用`push()`函数完成栈列表的插入](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)。

**示例**：

## C++

```cpp

// Loop to push element 
// into a stack 
for
    i in[0, n] 
    { 
        s.push(i) 
    } 

// Push Stack into the list 
ls.push_back(s); 

```

**遍历**：[使用](https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/)[迭代器](https://www.geeksforgeeks.org/iterators-c-stl/)进行栈列表中的遍历。

## C++

```cpp

// Loop to iterate over list 
for (iterator it = ls.begin(); 
     it != ls.end(); it++) { 

    // Stack of the List 
    stack<int> 
        st = *it; 

    while (!st.empty()) { 
        cout << st.top(); 
        st.pop(); 
    } 
} 

```

上面的代码使用开始迭代器`ls.begin()`和结束迭代器`ls.end()`在每个索引处遍历`list<stack<int>> ls`。 为了访问元素，它使用`*it`作为栈，而[指针](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)指向`list<stack<int>> ls`列表中的元素。

下面是说明栈列表中的插入和遍历的程序：

## C++

```cpp

// C++ program for implementation 
// of the lists of stack 

#include <bits/stdc++.h> 
using namespace std; 

// Function for printing the 
// elements in a list 
void showlist(list<stack<int> > ls) 
{ 

    // Traverse the list and 
    // print row wise stack 
    for (list<stack<int> >::iterator it1 
         = ls.begin(); 
         it1 != ls.end(); ++it1) { 

        // Copy rows in stack 
        stack<int> it2 = *it1; 

        // Print stack elements while 
        // it is not empty 
        while (!it2.empty()) { 
            cout << it2.top() << " "; 
            it2.pop(); 
        } 
        cout << endl; 
    } 
} 

// Driver Code 
int main() 
{ 
    // List of stacks 
    list<stack<int> > ls; 

    // Insert rows in list 
    for (int i = 0; i < 10; ++i) { 
        // Insert element in 
        // stack as column 
        stack<int> s; 

        for (int j = i; j < 10; j++) { 
            s.push(j); 
        } 

        ls.push_back(s); 
    } 

    cout << "List of stack is : \n"; 
    showlist(ls); 

    return 0; 
} 

```

**输出**：

```
List of stack is : 
9 8 7 6 5 4 3 2 1 0 
9 8 7 6 5 4 3 2 1 
9 8 7 6 5 4 3 2 
9 8 7 6 5 4 3 
9 8 7 6 5 4 
9 8 7 6 5 
9 8 7 6 
9 8 7 
9 8 
9

```

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。