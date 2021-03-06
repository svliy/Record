# 郑州大学2020-2021第一学期算法设计与分析-实验5（第三章）

## 1.

## 2.分弹珠

### Tag:[动态规划]

### 题面

> 把M个弹珠放到N个盘子里面（我们允许有的盘子为空），你能求出有多少种分法吗？（请注意，例如有三个盘子，我们将5,1,1和1,1,5，视为同一种分法）

### 输入格式:

> 输入包含多组测试样例。每组输入的第一行是一个整数t。 接下来t行，每行输入两个整数M和N，代表有M个弹珠和N个盘子。（0=<M<=20; 0<N<=20）

### 输出格式:

> 对于每对输入的M和N，输出有多少种方法。

### 输入样例:

> 在这里给出一组输入。例如：

```in
1
7 3
结尾无空行
```

### 输出样例:

> 在这里给出相应的输出。例如：

```out
8
结尾无空行
```

### 分析

​	题目要求就是将m个弹珠放到n个盘子内。

​	例子：

​	when m=3 n=2,
$$
(3,0) \\
(2,1) \\
$$
​	when m=3 n=3,
$$
(3,0,0) \\
(2,1,0) \\
(1,1,1)
$$
​	得到这样的结论：
$$
dp[m][n] =
\begin{cases} 
	dp[m][n-1]+dp[m-n][n],  & \text{if }m \geq n\\
	dp[m][m] 				& \text{if }m < n
\end{cases}
$$
​	当$m\geq n$时，m个弹珠分配给n个盘子的方案是在m个弹珠分配给n-1个盘子的基础上得到的，这个基础就是$dp[m][n-1]$，加上**占满n个盘子的方案**。这个方案的思路是，先在n个盘子上都放**1**个弹珠，接着进行分配，那么这个方案就是$dp[m-n][n]$。不太明白的，请带入具体的例子，比如最开始的$m=3\quad n=2$情形。

​	得到状态转移方程，就需要考虑线性规划的**边界条件**：

|      | 0    | 1    | 2    | 4    | 5    |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 0    |      | 1    | 1    | 1    | 1    |
| 1    |      | 1    | 1    | 1    | 1    |
| 2    |      | 1    | 入口 |      |      |
| 4    |      | 1    |      |      |      |
| 5    |      | 1    |      |      | 出口 |

​	这里对$row = 0 $的赋值，是因为$m==n$时,需要考虑情况$dp[m][n]=dp[m][n-1]+dp[0][n]$。

### 代码

```c++
#include <bits/stdc++.h>
using namespace std;
#define N 21
int main(){
    int t,m,n;
    int dp[N][N] = {0};
    cin >> t;
    while(t--){
        cin >> m >> n;
        //初始化
        for(int i=0;i<N;i++){
            dp[0][i] = 1;
            dp[i][1] = 1;//苹果放在1个盘子里
            dp[1][i] = 1;//1个苹果
        }
        for(int i = 2; i <= m; i++){
            for (int  j = 2; j <= n; j++)
            {
                if(i >= j)
                    dp[i][j] = dp[i][j-1] + dp[i-j][j];
                else
                    dp[i][j] = dp[i][i];
            }
        }
        cout << dp[m][n] << endl;
    }
    return 0;    
}
```

# 郑州大学2020-2021第一学期算法设计与分析-实验6（第四章）

## 1 月饼

Tag

### 代码

