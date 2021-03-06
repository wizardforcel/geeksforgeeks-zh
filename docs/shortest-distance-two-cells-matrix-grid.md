# 矩阵或网格中两个单元之间的最短距离

> 原文： [https://www.geeksforgeeks.org/shortest-distance-two-cells-matrix-grid/](https://www.geeksforgeeks.org/shortest-distance-two-cells-matrix-grid/)

给定一个`N * M`阶矩阵。 查找从源单元格到目标单元格的最短距离，仅遍历有限的单元格。 您也只能向上，向下，向左和向右移动。 如果找到，则输出距离，否则为 -1。

`s`代表“源”，`d`代表“目的地”，`*`代表您可以旅行的单元格，`0`代表您不能旅行的单元格，此问题仅适用于单个来源和目的地。

例子：

```
Input : {'0', '*', '0', 's'},
        {'*', '0', '*', '*'},
        {'0', '*', '*', '*'},
        {'d', '*', '*', '*'}
Output : 6

Input :  {'0', '*', '0', 's'},
         {'*', '0', '*', '*'},
         {'0', '*', '*', '*'},
         {'d', '0', '0', '0'}
Output :  -1

```



这个想法是对矩阵单元进行 [BFS（优先搜索）](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)。 请注意，如果图形未加权，我们总是可以使用 BFS 查找最短路径。

1.  将每个单元格及其行，列值和到源单元格的距离存储为节点。

2.  从源单元启动 BFS。

3.  制作一个访问数组，所有数组都具有`false`值，但不能遍历被分配为`true`值的 0 单元格除外。

4.  每次移动时都要持续更新到源值的距离。

5.  到达目标位置时返回的距离，否则返回 -1（源和目标之间不存在路径）。

```

// C++ Code implementation for above problem 
#include <bits/stdc++.h> 
using namespace std; 

#define N 4 
#define M 4 

// QItem for current location and distance 
// from source location 
class QItem { 
public: 
    int row; 
    int col; 
    int dist; 
    QItem(int x, int y, int w) 
        : row(x), col(y), dist(w) 
    { 
    } 
}; 

int minDistance(char grid[N][M]) 
{ 
    QItem source(0, 0, 0); 

    // To keep track of visited QItems. Marking 
    // blocked cells as visited. 
    bool visited[N][M]; 
    for (int i = 0; i < N; i++) { 
        for (int j = 0; j < M; j++) 
        { 
            if (grid[i][j] == '0') 
                visited[i][j] = true; 
            else
                visited[i][j] = false; 

            // Finding source 
            if (grid[i][j] == 's') 
            { 
               source.row = i; 
               source.col = j; 
            } 
        } 
    } 

    // applying BFS on matrix cells starting from source 
    queue<QItem> q; 
    q.push(source); 
    visited[source.row][source.col] = true; 
    while (!q.empty()) { 
        QItem p = q.front(); 
        q.pop(); 

        // Destination found; 
        if (grid[p.row][p.col] == 'd') 
            return p.dist; 

        // moving up 
        if (p.row - 1 >= 0 && 
            visited[p.row - 1][p.col] == false) { 
            q.push(QItem(p.row - 1, p.col, p.dist + 1)); 
            visited[p.row - 1][p.col] = true; 
        } 

        // moving down 
        if (p.row + 1 < N && 
            visited[p.row + 1][p.col] == false) { 
            q.push(QItem(p.row + 1, p.col, p.dist + 1)); 
            visited[p.row + 1][p.col] = true; 
        } 

        // moving left 
        if (p.col - 1 >= 0 && 
            visited[p.row][p.col - 1] == false) { 
            q.push(QItem(p.row, p.col - 1, p.dist + 1)); 
            visited[p.row][p.col - 1] = true; 
        } 

         // moving right 
        if (p.col + 1 < M && 
            visited[p.row][p.col + 1] == false) { 
            q.push(QItem(p.row, p.col + 1, p.dist + 1)); 
            visited[p.row][p.col + 1] = true; 
        } 
    } 
    return -1; 
} 

// Driver code 
int main() 
{ 
    char grid[N][M] = { { '0', '*', '0', 's' }, 
                        { '*', '0', '*', '*' }, 
                        { '0', '*', '*', '*' }, 
                        { 'd', '*', '*', '*' } }; 

    cout << minDistance(grid); 
    return 0; 
} 

```

输出：

```
6

```



