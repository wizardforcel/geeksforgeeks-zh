# 给定大小为`n`的数组和数字`k`，找到出现超过`n / k`次的所有元素

> 原文： [https://www.geeksforgeeks.org/given-an-array-of-of-size-n-finds-all-the-elements-that-appear-more-than-nk-times/](https://www.geeksforgeeks.org/given-an-array-of-of-size-n-finds-all-the-elements-that-appear-more-than-nk-times/)

给定大小为`n`的数组，找到数组中出现`n / k`次以上的所有元素。 例如，如果输入数组为`{3, 1, 2, 2, 1, 2, 2, 3, 3}`，`k`为 4，则输出应为`[2, 3]`。 请注意，数组的大小为 8（或`n = 8`），因此我们需要查找所有出现超过 2（或`8/4`）次的元素。 有两个元素出现两次以上，即 2 和 3。



**简单方法**是一个接一个地选择所有元素。 对于每个拾取的元素，通过遍历数组来计数它的出现，如果`count`大于`n / k`，则打印该元素。 该方法的时间复杂度为`O(n^2)`。

更好的解决方案是**使用排序**。 首先，使用`O(nLogn)`算法对所有元素进行排序。 数组排序后，我们可以在数组的线性扫描中找到所有必需的元素。 因此，此方法的总体时间复杂度为`O(nLogn)+O(n)`，即`O(nLogn)`。

以下是一个有趣的`O(nk)`解决方案：

我们可以使用`O(k-1)`多余空间来解决`O(nk)`时间中的上述问题。 请注意，输出中的元素不得超过`k-1`个（为什么？）。 该算法主要包括三个步骤。

1.  创建大小为`k-1`的临时数组，以存储元素及其计数（输出元素将在这`k-1`个元素中）。 以下是临时数组元素的结构。

```
struct eleCount {
    int element;
    int count;
}; 
struct eleCount temp[]; 
```

此步骤需要`O(k)`时间。

2.  遍历输入数组并为每个遍历的元素更新`temp[]`（添加/删除元素或增加/减少计数）。 数组`temp[]`在每个步骤中存储潜在`k-1`个候选对象。 此步骤需要`O(nk)`时间。

3.  迭代最终`k-1`个潜在候选对象（存储在`temp[]`中）。 或每个元素，请检查其实际计数是否大于`n / k`。 此步骤需要`O(nk)`时间。

主要步骤是步骤 2，如何在每个点上保持`k-1`个潜在候选者？ 步骤 2 中使用的步骤类似于著名的游戏： [俄罗斯方块](http://en.wikipedia.org/wiki/Tetris)。 我们在俄罗斯方块中将每个数字视为一个部分，这属于我们的临时数组`temp[]`。 我们的任务是尝试将相同的数字堆叠在同一列上（临时数组中的计数增加）。

```
Consider k = 4, n = 9 
Given array: 3 1 2 2 2 1 4 3 3 

i = 0
         3 _ _
temp[] has one element, 3 with count 1

i = 1
         3 1 _
temp[] has two elements, 3 and 1 with 
counts 1 and 1 respectively

i = 2
         3 1 2
temp[] has three elements, 3, 1 and 2 with
counts as 1, 1 and 1 respectively.

i = 3
         - - 2 
         3 1 2
temp[] has three elements, 3, 1 and 2 with
counts as 1, 1 and 2 respectively.

i = 4
         - - 2 
         - - 2 
         3 1 2
temp[] has three elements, 3, 1 and 2 with
counts as 1, 1 and 3 respectively.

i = 5
         - - 2 
         - 1 2 
         3 1 2
temp[] has three elements, 3, 1 and 2 with
counts as 1, 2 and 3 respectively. 
```

现在出现了一个问题，当`temp[]`满时该怎么办，我们看到一个新元素–我们从元素栈中删除最下面一行，即，我们在`temp[]`中将每个元素的数量减少 1。 我们忽略当前元素。

```
i = 6
         - - 2 
         - 1 2 
temp[] has two elements, 1 and 2 with
counts as 1 and 2 respectively.

i = 7
           - 2 
         3 1 2 
temp[] has three elements, 3, 1 and 2 with
counts as 1, 1 and 2 respectively.

i = 8          
         3 - 2
         3 1 2 
temp[] has three elements, 3, 1 and 2 with
counts as 2, 1 and 2 respectively.

```

最后，我们在`temp[]`中最多有`k-1`个数字。 `temp`中的元素为`{3, 1, 2}`。 请注意，`temp[]`中的计数现在已无用，仅在步骤 2 中才需要计数。现在我们需要检查`temp[]`中元素的实际计数是否大于`n / k`（`9/4`）。 元素 3 和 2 的计数大于`9/4`。 因此，我们打印 3 和 2。

请注意，该算法不会遗漏任何输出元素。 可能有两种可能性，许多事件在一起或分布在整个数组中。 如果出现的次数在一起，则计数将很高，并且不会变为 0。如果出现的次数分散，则元素将再次以`temp[]`出现。 以下是上述算法的 C++ 实现。

```

// A C++ program to print elements with count more than n/k 
#include<iostream> 
using namespace std; 

// A structure to store an element and its current count 
struct eleCount 
{ 
    int e;  // Element 
    int c;  // Count 
}; 

// Prints elements with more than n/k occurrences in arr[] of 
// size n. If there are no such elements, then it prints nothing. 
void moreThanNdK(int arr[], int n, int k) 
{ 
    // k must be greater than 1 to get some output 
    if (k < 2) 
       return; 

    /* Step 1: Create a temporary array (contains element 
       and count) of size k-1\. Initialize count of all 
       elements as 0 */
    struct eleCount temp[k-1]; 
    for (int i=0; i<k-1; i++) 
        temp[i].c = 0; 

    /* Step 2: Process all elements of input array */
    for (int i = 0; i < n; i++) 
    { 
        int j; 

        /* If arr[i] is already present in 
           the element count array, then increment its count */
        for (j=0; j<k-1; j++) 
        { 
            if (temp[j].e == arr[i]) 
            { 
                 temp[j].c += 1; 
                 break; 
            } 
        } 

        /* If arr[i] is not present in temp[] */
        if (j == k-1) 
        { 
            int l; 

            /* If there is position available in temp[], then place  
              arr[i] in the first available position and set count as 1*/
            for (l=0; l<k-1; l++) 
            { 
                if (temp[l].c == 0) 
                { 
                    temp[l].e = arr[i]; 
                    temp[l].c = 1; 
                    break; 
                } 
            } 

            /* If all the position in the temp[] are filled, then  
               decrease count of every element by 1 */
            if (l == k-1) 
                for (l=0; l<k; l++) 
                    temp[l].c -= 1; 
        } 
    } 

    /*Step 3: Check actual counts of potential candidates in temp[]*/
    for (int i=0; i<k-1; i++) 
    { 
        // Calculate actual count of elements  
        int ac = 0;  // actual count 
        for (int j=0; j<n; j++) 
            if (arr[j] == temp[i].e) 
                ac++; 

        // If actual count is more than n/k, then print it 
        if (ac > n/k) 
           cout << "Number:" << temp[i].e 
                << " Count:" << ac << endl; 
    } 
} 

/* Driver program to test above function */
int main() 
{ 
    cout << "First Test\n"; 
    int arr1[] = {4, 5, 6, 7, 8, 4, 4}; 
    int size = sizeof(arr1)/sizeof(arr1[0]); 
    int k = 3; 
    moreThanNdK(arr1, size, k); 

    cout << "\nSecond Test\n"; 
    int arr2[] = {4, 2, 2, 7}; 
    size = sizeof(arr2)/sizeof(arr2[0]); 
    k = 3; 
    moreThanNdK(arr2, size, k); 

    cout << "\nThird Test\n"; 
    int arr3[] = {2, 7, 2}; 
    size = sizeof(arr3)/sizeof(arr3[0]); 
    k = 2; 
    moreThanNdK(arr3, size, k); 

    cout << "\nFourth Test\n"; 
    int arr4[] = {2, 3, 3, 2}; 
    size = sizeof(arr4)/sizeof(arr4[0]); 
    k = 3; 
    moreThanNdK(arr4, size, k); 

    return 0; 
} 

```

输出：

```
First Test
Number:4 Count:3

Second Test
Number:2 Count:2

Third Test
Number:2 Count:2

Fourth Test
Number:2 Count:2
Number:3 Count:2
```

时间复杂度：`O(nk)`。

辅助空间：`O(k)`。

通常会问到此问题的变体，找到所有在`O(n)`时间复杂度和`O(1)`额外空间中出现`n / 3`次或`n / 4`次的元素。

**散列**也是一种有效的解决方案。 有了良好的哈希函数，我们平均可以在`O(n)`时间上解决上述问题。 散列所需的额外空间将大于`O(k)`。 同样，哈希不能用于解决`O(1)`额外空间的上述变化。

**练习**：

可以使用比用于`k-1`个元素的辅助存储的数组更合适的数据结构，在`O(nLogk)`时间内解决上述问题。 建议使用`O(nLogk)`方法。

