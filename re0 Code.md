## https://v.douyu.com/author/PDAPVoKO3wxN

##  LT 231 2的幂

&emsp;**给定一个整数，编写一个函数来判断它是否是 2 的幂次方。**
```
code:
class Solution {
public:
    bool isPowerOfTwo(int n) {

            return ((n>0)&&((n&-n)==n));
    }
};
```

---

解题思路：
    ==lowbit== 的操作为 n&-n 返回 二进制的n的从左到右的第一个‘1’出现及其之后的数n。
    如果lowbit返回的和原来的数n相同，则说明n是类似于100000的数
    ，==并且2的n次幂的二进制也为100000类似的数==。
## **LT 136单身数**
&emsp;  **给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。**

说明：
你的算法应该具有线性时间复杂度。你可以不使用额外空间来实现吗？

示例 1:

```
输入: [2,2,1]
输出: 1
```

```
Code:
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res=0;
        for(auto x:nums)res^=x;
        return res;
    }
};
解题思路：
    在c++中位运算‘^’异或， a^a=0 ,0^a=a; 异或可以看成是不进位的加法，并且异或符合结合律和分配率
    举个例子 [1,1,2,2,3,3,4]
    1^1^2^2^3^3^4
    1^1=0
    2^2=0
    .....
    最后剩下0^4=4就可以求出这个单身数了。
```
---
## LT 476 数字的补数
题目描述：给定一个正整数，输出它的补数。补数是对该数的二进制表示取反。
示例 1:


```
输入: 5
输出: 2
解释: 5 的二进制表示为 101（没有前导零位），其补数为 010。所以你需要输出 2 。
```

```
//Code：
class Solution {
public:
    int findComplement(int num) {
        int res=0,k=0;
        for(int i=num;i;i>>=1)
        {
            res+=!(i&1)<<k++;
        }
        return res;
    }
};
//C++中int 是32个bit位比如5，000000000000000101，取反可以为是111111111111111111010，但是题目要求是101，取反直接是010。
解题思路
    每次求出nums的最后一位是什么，用当前的nums&1即可，
因为是求补码所以要！(num&1) ，因为要求的是10进制数，
每次还要将res左移一位用k表示当前移了几位，并且将nums左移一位。
```
---
## LT 137 Single number II
题目描述
```
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现了三次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:

输入: [2,2,3,2]
输出: 3
```
```
Code:
    class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res=0;
        for(int bit=0;bit<32;bit++)
        {
            int counter=0;
            for(int i=0;i<nums.size();i++)
            {
                counter+=(nums[i]&1);
                nums[i]>>=1;
            }
            res+=(counter%3)<<bit;
            
        }
        return res;
    }
};
```
解题思路

举个例子:[2,2,2,3];

```
2的二进制 00000000010
          00000000010
          00000000010
3的二进制 00000000011
```

把vector中的每个数的每一位依次相加到counter中，因为int有32位

所以共循环32次，内层循环是求vector<nums>中每个数的每位相加

因为有题目是3次重复的数，只要将counter%3就可以求出结果的那一位是什么，再将他们转换为10进制数。

---
## LT 260 Single of number III
**给定一个整数数组 nums，其中恰好有两个元素只出现一次，其余所有元素均出现两次。 找出只出现一次的那两个元素。**
```
示例 :

输入: [1,2,1,3,2,5]
输出: [3,5]
注意：

结果输出的顺序并不重要，对于上面的例子， [5, 3] 也是正确答案。
你的算法应该具有线性时间复杂度。你能否仅使用常数空间复杂度来实现？
```
```c++
Code:
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {

        int s=0,k=0;
        for(int i=0;i<nums.size();i++)s^=nums[i];
        int s2=0;
        while(!(s>>k&1))k++;
        for(auto x:nums)
            if(x>>k&1)s2^=x;
        return vector<int>({s2,s^s2});

/*
1:0000000000001
1:0000000000001
2:0000000000010
2:0000000000010
3:0000000000011
5:0000000000101
*/
    }
};
```



解题思路：异或和有这样的性质，类似于消消乐，会将一样的两个数消掉，即a^a=0，根据题目描述，nums中有两个不一样的数。

我们可以，找到这两个数是从哪一位开始不同的，把那一位为1的分成一堆，为0的又分成一堆，分别对这两个堆进行异或，在取并集即使结果。

现在谈谈代码，先求一遍所有数的异或和，我们可以预见得是其最终结果就是我们要求的那两个数的异或和，假设该数为c，然后继续找到c的二进制中为1的是在哪一位。即是不同的那一位，接着利用这一位为1的异或，即可求出堆为1的堆s1，其实最后没必要再通过循环去求堆0
直接用c^s1=s2,(s1s2分别为要求的两个数)
// c=s1 ^ s2  c^s1 <=> s1 ^ s1 ^ s2 -> 0 ^ s2 -> s2



---

## LT [371. 两整数之和](https://leetcode-cn.com/problems/sum-of-two-integers/)

**题目描述：不使用运算符 + 和 - ，计算两整数 a 、b 之和。**

```c++
示例 1:

输入: a = 1, b = 2
输出: 3
示例 2:

输入: a = -2, b = 3
输出: 1
```

```c++
Code：
class Solution {
public:
    int getSum(int a, int b) {
        if(!b)return a;
        int sum=a^b,carry=unsigned(a&b)<<1;//为什么要强制转换为unsigned呢？:lt不支持负数的<<操作
        return getSum(sum,carry);
    }
};
```

**解题思路：c++中异或可以看成不进位的加法，可以先让a^b=c(假设为结果为c)，因为是不进位的加法所以，c<=a+b，一定成立。**

**也就是代码中的sum，那carry代表的就是没有进位而造成的差值。递归计算，直到传入的参数不需要进位，carry==0**

​	**举个例子：**

```
a = 	1101 // 13
b =  	1001 //  9
a^b = 	0100 //  4
a&b =   1001 //  9
a&b<<1=10010 // 18
(a&b<<1) +(a^b) = 10110 //22
```

---

## LT [201. 数字范围按位与](https://leetcode-cn.com/problems/bitwise-and-of-numbers-range/)

**给定范围 [m, n]，其中 0 <= m <= n <= 2147483647(2^30 - 1)，返回此范围内所有数字的按位与（包含 m, n 两端点）。**

```
示例 1: 

输入: [5,7]
输出: 4

示例 2:

输入: [0,1]
输出: 0
```

解题思路:

&操作有一个神奇的地方，只要有一位是0其余便全是0，利用这性质，找到第i位为1，然后让1<<i位 ，如此循环m的位数次。

还有一个问题，就是如何找到[m,n]之间的第i位是不是0呢，举个例子

```c++
	m=101010'1'0011  假设''为第i位
比m大的且第i位为0 最小的数是什么呢
解 把第i位加上1且让  第i位后都清零
	x= 101011'0'0000 即为所求。

     实际操作

 但m1又该如何求得呢
 1<<i         			得m3=  000000 1 0000
 (1<<i)-1	 			m3-1=  000000 0 1111
 ~((1<<i)-1)     		m1=    111111 1 0000
m&~((1<<i)-1) 			m2=    101010 1 0000
m&~((1<<i)-1)+(1<<i)  	 x=     101011'0'0000
if( m & ~((1<<i)-1))+(1<<i) > n )反证法 如果 m & ~((1<<i)-1))+(1<<i)<=n 则说明在[m,n]之间第i位为0，则&后必有0，
    反之 m & ~((1<<i)-1))+(1<<i) > n则说明第i位&后是1.


class Solution {
public:
    int rangeBitwiseAnd(int m, int n) {
        int res = 0;
        for (int i = 0; (1ll << i) <= m; i ++ )
            if (m >> i & 1)
            {
                if ((m & ~((1 << i) - 1ll)) + (1 << i) > n)
                    res += 1 << i;
            }
        return res;
    }
};

```

---

## LT  [ 477. 汉明距离总和](https://leetcode-cn.com/problems/total-hamming-distance/)

**题目描述：**

**两个整数的 [汉明距离](https://baike.baidu.com/item/汉明距离/475174?fr=aladdin) 指的是这两个数字的二进制数对应位不同的数量。**

**计算一个数组中，任意两个数之间汉明距离的总和。**

```
示例:

输入: 4, 14, 2

输出: 6

解释: 在二进制表示中，4表示为0100，14表示为1110，2表示为0010。（这样表示是为了体现后四位之间关系）
所以答案为：
HammingDistance(4, 14) + HammingDistance(4, 2) + HammingDistance(14, 2) = 2 + 2 + 2 = 6.
注意:

数组中元素的范围为从 0到 10^9。
数组的长度不超过 10^4。
```

 **解体思路：**

```
4: 	01 0 0//二进制表示
14:	11 1 0
2:	00 1 0
总结的来说，在某一位整个数组中的汉明距离就是这一位为1的个数乘这一位为0的个数
以第一位为例：0 1 1
0的个数：x=1 
1的个数：y=2
这一位的汉明距离为 x*y
再将num数组的每一位的汉明距离求和即可。
```

```c++
Code:
class Solution {
public:
    int totalHammingDistance(vector<int>& nums) {
        int res=0;
        for(int i=0;i<30;i++)
        {
            int ones=0;//1的个数
            for(auto x: nums)
            {
                if(x>>i&1)ones++;
            }
            res+=ones*(nums.size()-ones);
        }
        return res;
    }
};
```

---

## LT[421. 数组中两个数的最大异或值](https://leetcode-cn.com/problems/maximum-xor-of-two-numbers-in-an-array/)

**题目描述：**

**给定一个非空数组，数组中元素为 a0, a1, a2, … , an-1，其中 0 ≤ ai < 231 。**

**找到 ai 和aj 最大的异或 (XOR) 运算结果，其中0 ≤ i,  j < n 。**

**你能在O(n)的时间解决这个问题吗？**

**解题思路：**

```c++
	使用数据结构Trie树便可以解决， Trie，又经常叫前缀树，字典树。
	Trie树通常用来存储字符，但也可以存储二进制0,1，这也是此题的解决办法。
	求数组中两个数的异或和的最大值，可以先建立Trie树，再循环一遍数组，把数组中的所有数的二进制存入Trie树中，循环过程中利用贪心的思想，从最高位开始循环，就是宁可要高位的1，也不要次高位的1，打个比方10000>01111。如果实在没有办法也只能退了求其次。
```

![image-20200923225735233](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20200923225735233.png)

//图中Bit表示二进制中的第几位

```c++
Code:
class Solution
{
public:
    struct Nodes
    {
        int son[2];
    };
    vector<Nodes> nodes;
    int findMaximumXOR(vector<int> &nums)
    {
        nodes.push_back({0, 0});//先向Trie存入一个Nodes{0,0}
        for (auto x : nums)//遍历数组
        {
            int p = 0;//指针
            for (int i = 30; i >= 0; i--)//数组中的数存入Trie树中。
            {
                int t = x >> i & 1;
                if (!nodes[p].son[t])//如果当前节点p的son[t]不存在则创建一个。
                {
                    nodes.push_back(Nodes({0, 0}));
                    nodes[p].son[t] = nodes.size() - 1;//p的本质存的是下标。
                }
                p = nodes[p].son[t];
            }
        }
        int res = 0;//通过此Trie树的叶节点并不是存的那个数，整个Trie树存的就是二进制。
        for (auto x : nums)
        {
            int p = 0, max_xor = 0;
            for (int i = 30; i >= 0; i--)
            {
                int t = x >> i & 1;
                if (nodes[p].son[!t])//如果x的第i位不同则^的结果为1，(1<<i)否则直接跳到下一个节点。
                {
                    p = nodes[p].son[!t];
                    max_xor += 1 << i;
                }
                else
                {
                    p = nodes[p].son[t];
                    //(0<<i，结果还是0,所以没必要写出来)
                }
            }
            res = max(res, max_xor);
        }
        return res;
    }
};
```

## LT [111. 二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

**题目描述**：

**给定一个二叉树，找出其最小深度。**

**最小深度是从根节点到最近叶子节点的最短路径上的节点数量。**

**说明: 叶子节点是指没有子节点的节点。**

**示例:**

**给定二叉树 [3,9,20,null,null,15,7],**



```c++
    3
   / \
  9  20
    /  \
   15   7
```

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * }; 
 */
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(!root)return 0;//递归基 到了叶节点。
        int left=minDepth(root->left);//递归搜索左右节点。查看左右子树高度
        int right=minDepth(root->right);
        if(!left||!right)return left+right+1;//如果左子树或右子树有一个不存在的话，则可以直接
        //return left+right+1 因为left和right有一个是0，避免if语句。
        return min(left,right)+1;
    }
};
```

```c++
解题思路：
递归的解法，很难用具体的语言方式去描述，需要注意几点
1.	TreeNode(int x) : val(x), left(NULL), right(NULL) {}
上述构造函数将叶节点的左右节点定义为NULL，这也为代码中的递归基做了铺垫，当递归到叶节点时，叶节点的左右儿子都是null则到达
递归基返回0。
```

## [剑指 Offer 55 - I. 二叉树的深度](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

**题目描述：**

**输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。**

**例如：**

**给定二叉树 [3,9,20,null,null,15,7]，**

```c++
   3
   / \
  9  20
    /  \
   15   7			返回它的最大深度 3 。
```

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(!root)return 0;
        int left=maxDepth(root->left);
        int right=maxDepth(root->right);
        return max(right,left)+1;

    }
};
```

```c++
//解题思路：

//可以直接仿照最小二叉树深度那个题目，只不过不再需控制
    if(!left||!right)return left+right+1;
```

---

## [LT 279. 完全平方数](https://leetcode-cn.com/problems/perfect-squares/)

**题目描述：**

**给定正整数 *n*，找到若干个完全平方数（比如 `1, 4, 9, 16, ...`）使得它们的和等于 *n*。你需要让组成和的完全平方数的个数最少。**

```c++
/*
示例 1:

输入: n = 12
输出: 3 
解释: 12 = 4 + 4 + 4.
示例 2:

输入: n = 13
输出: 2
解释: 13 = 4 + 9.
*/
```

```c++
Code:代码是典型的bfs模版
class Solution {
public:
    int numSquares(int n) {
        queue<int> q;
        vector<int> dist(n+1,INT_MAX);//将dist初始化为无穷大
        q.push(0);//从0开始的bfs
        dist[0]=0;//
        while(q.size())
        {
            int t=q.front();
            q.pop();
            if(t==n)return dist[t];
            for(int i=1;i*i+t<=n;i++)//i*i ：题目要求是平方数
            {
                int j=i*i+t;
                if(dist[j]>dist[t]+1)//因为j>t，如果dist[j]>dist[t]+1，便可以用dist[t]+1更新dist[j]
                {
                    dist[j]=dist[t]+1;
                    q.push(j);//将j放入队列中，再用dist[j]去更新大于j的数。
                }
            }
        }
        return 0;
    }   
};
```

**解题思路：**

**BFS问题， 用一个队列存，因为bfs有最小性质。建立一个图，每个平方数是一个节点，节点之间用权重为‘1‘的边相连。(权重是1：**

**因为题目要求求出最小平方数的个数。也就是代码中dist[]所存储的，)**

---





## [LT733. 图像渲染](https://leetcode-cn.com/problems/flood-fill/) -Flood Fill

**题目描述：**

**有一幅以二维整数数组表示的图画，每一个整数表示该图画的像素值大小，数值在 0 到 65535 之间。**

**给你一个坐标 (sr, sc) 表示图像渲染开始的像素值（行 ，列）和一个新的颜色值 newColor，让你重新上色这幅图像。**

**为了完成上色工作，从初始坐标开始，记录初始坐标的上下左右四个方向上像素值与初始坐标相同的相连像素点，接着再记录这四个方向上符合条件的像素点与他们对应四个方向上像素值与初始坐标相同的相连像素点，……，重复该过程。将所有有记录的像素点的颜色值改为新的颜色值。**

**最后返回经过上色渲染后的图像。**

```c++
Flood Fill ：可以在网格图中搜索到一个连通块。
输入: 
image = [[1,1,1],[1,1,0],[1,0,1]]
sr = 1, sc = 1, newColor = 2
输出: [[2,2,2],[2,2,0],[2,0,1]]
解析: 
在图像的正中间，(坐标(sr,sc)=(1,1)),
在路径上所有符合条件的像素点的颜色都被更改成2。
注意，右下角的像素没有更改为2，
因为它不是在上下左右四个方向上与初始点相连的像素点。

/*
example	:	
		1 1 1
		1 1 0
		1 0 1
ans  	:
		2 2 2
		2 2 0
		2 0 1
*/
```

~~~c++
```c++
Code:
class Solution
{
public:
    vector<vector<int>> floodFill(vector<vector<int>> &image, int sr, int sc, int newColor)
    {
        if (image.empty() || image[0].empty())//特判二维数组是否为空
            return image;
        int dx[4] = {-1, 0, 1, 0}, dy[4] = {0, 1, 0, -1};
        int oldColor = image[sr][sc];//记录原来的颜色oldColor
        if (oldColor == newColor)//原颜色==新颜色 原数组不需改变。
            return image;
        image[sr][sc] = newColor;
        for (int i = 0; i < 4; i++)
        {
            int x = sr + dx[i], y = sc + dy[i];
            if (x >= 0 && x < image.size() && y >= 0 && y < image[0].size() && image[x][y] == oldColor)
                floodFill(image, x, y, newColor);
        }
        return image;
    }
};

~~~

```c++
解题思路:

bfs，dfs都可以，但dfs有着易于理解的递归。从开始给的 x=sr，y=sc，开始递归，没有显式的递归基，可以理解为到最后 return image 时整个函数就结束了。

需要注意：

1.判断是否vector<vector<int>是空的，image.empty() || image[0].empty()

2.当oldColor==newcolor 递归会一直进行下去，从而导致爆栈，所以要特判。

3.当做网格题的图时，需要遍历上下左右可以使用 int dx[4] = {-1, 0, 1, 0}, dy[4] = {0, 1, 0, -1};
再循环4次，相比用if语句的代码更加简洁。


```

---

## [LT200. 岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

**题目描述：**

**给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。**

**岛屿总是被水包围，并且每座岛屿只能由水平方向或竖直方向上相邻的陆地连接形成。**

**此外，你可以假设该网格的四条边均被水包围。**

```c++
示例 1:

输入:
[
['1','1','1','1','0'],
['1','1','0','1','0'],
['1','1','0','0','0'],
['0','0','0','0','0']
]
输出: 1
示例 2:

输入:
[
['1','1','0','0','0'],
['1','1','0','0','0'],
['0','0','1','0','0'],
['0','0','0','1','1']
]
输出: 3
解释: 每座岛屿只能由水平和/或竖直方向上相邻的陆地连接而成。

```



解题思路：求图中连通块的个数。

遍历一遍数组，只要遇到 '1'就把和它相邻的以及它自己变成 ‘0’，这样问题就变成了求解遇到 ‘1’ 的次数。

`````````c++
Code:
class Solution {
public:
        int n,m;
        int numIslands(vector<vector<char>>& grid) {
        if(grid.empty())return 0;//特判grid为空，很重要
        n=grid.size();//n，m分别为grid的行和列的长度。
        m=grid[0].size();
        int  res =0;    
            for(int i=0;i<n;i++)//遍历
        {
            for(int j=0;j<m;j++)
            {
                  if(grid[i][j]=='1')
                  {  
                      res++;
                      dfs(grid,i,j);
                  }
            }
        }
        return res; 
    }
    void dfs(vector<vector<char>>& grid,int x,int y)
    {
        int dx[4]={-1,0,1,0},dy[4]={0,-1,0,1};
        grid[x][y]='0';
        for(int i=0;i<4;i++)
        {
            int a=x+dx[i],b=y+dy[i];
            if(a>=0&&a<n&&b<m&&b>=0&&grid[a][b]=='1')
                dfs(grid,a,b);
        }
    }
};
`````````

---

## LT[130. 被围绕的区域](https://leetcode-cn.com/problems/surrounded-regions/)

**题目描述：**

**给定一个二维的矩阵，包含 `'X'` 和 `'O'`（字母 O）。**

**找到所有被 `'X'` 围绕的区域，并将这些区域里所有的 `'O'` 用 `'X'` 填充。**	

 ```c++
示例:

'X X X X
'X O O X
'X X O X
'X O X X
运行你的函数后，矩阵变为：

'X X X X
'X X X X
'X X X X
'X O X X
解释:

被围绕的区间不会存在于边界上，换句话说，任何边界上的 'O' 都不会被填充为 'X'。 任何不在边界上，或不与边界上的 'O' 相连的 'O' 最终都会被填充为 'X'。如果两个元素在水平或垂直方向相邻，则称它们是“相连”的。

 ```

**解体思路:**

**把可以从边界上遍历到的 `'O'`，都标记一下(可以标记成 `‘Y’`)，然后再次遍历，把未标记的`'O'`都变成`'x'`。**

```c++
Code:
class Solution {
public:
    int n,m;
    void solve(vector<vector<char>>& board) {
        if(board.empty()||board[0].empty())return;
        n=board.size(),m=board[0].size();
        for(int i=0;i<n;i++)//遍历边界，上下两条边。
        {
            if(board[i][0]=='O')dfs(board,i,0);
            if(board[i][m-1]=='O')dfs(board,i,m-1);
        }
        for(int i=0;i<m;i++)//遍历边界，左右两条边。
        {
            if(board[0][i]=='O')dfs(board,0,i);
            if(board[n-1][i]=='O')dfs(board,n-1,i);
        }
        /*for(int i=0;i<n;i++)
            for(int j=0;j<m;j++)
                if(board[i][j]=='O')board[i][j]='X';
        for(int i=0;i<n;i++)
            for(int j=0;j<m;j++)
                if(board[i][j]=='Y')board[i][j]='O';*/
        //更优美简洁的遍历方法，避免了两次循环。
         for(int i=0;i<n;i++)
            for(int j=0;j<m;j++)
                board[i][j]=borad[i][j]=='Y'?'O':'X';
    }
    void dfs(vector<vector<char>>& board,int x,int y)
    {
        int dx[4]={-1,0,1,0},dy[4]={0,1,0,-1};
        board[x][y]='Y';
        for(int i=0;i<4;i++)
        {
            int a=x+dx[i],b=y+dy[i];
            if(a>=0&&a<n&&b>=0&&b<m&&board[a][b]=='O')
            {
                dfs(board,a,b);
            }
        }
    }
};
```

---

## [LT784. 字母大小写全排列](https://leetcode-cn.com/problems/letter-case-permutation/)



**题目描述：给定一个字符串`S`，通过将字符串`S`中的每个字母转变大小写，我们可以获得一个新的字符串。返回所有可能得到的字符串集合。**

```c++
示例：
输入：S = "a1b2"
输出：["a1b2", "a1B2", "A1b2", "A1B2"]

输入：S = "3z4"
输出：["3z4", "3Z4"]

输入：S = "12345"
输出：["12345"]

```

```c++
Code:
class Solution {
public:
    vector<string> ans;//记录答案
    vector<string> letterCasePermutation(string S) {
        dfs(S,0);
        return ans;
    }
    
    void  dfs(string S,int u)
    {
        if(u==S.size())//递归基
        {
            ans.push_back(S);
            return ;
        }
        dfs(S,u+1);//变或不变，这就是不变的情况。
        
        if(S[u]>='A')//因为A的是accii是65，数字1的65，a的是97，所以只要S[u]>=65，及说明是字母。
      //if(!isdigit(S[u]))这种写法也可以。
        {
            S[u]^=32;//A或a，大写字母或小写字母^32，可以相互转换，具体证明看下。
            dfs(S,u+1);
            S[u]^=32;//还原现场，没必要
        }
    }
};

```

解题思路:

dfs,每种情况看做一个图节点。

```
A=65 1'0'00001
a=97 1'1'00001
  32 0'1'00000
它们的第 5 位是不同的，a或A^32时，就会转换。
```

---

## LT[77. 组合](https://leetcode-cn.com/problems/combinations/)

**题目描述：**

**给定两个整数 *n* 和 *k*，返回 1 ... *n* 中所有可能的 *k* 个数的组合。**

```c++
示例:

输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]

```

```c++
Code:
class Solution {
public:
    vector<vector<int>> ans;//答案vector
    vector<vector<int>> combine(int n, int k) {
        vector<int> path;//记录方案的中间结果
        dfs(path,1,n,k);//参数:中间过程，从那开始，总个数，还需要几个数
        return ans;
    }
    void dfs(vector<int>&path,int start,int n,int k)
    {
        if(!k)//如果数够了
        {
            ans.push_back(path);
            return;
        }
        for(int i=start;i<=n;i++)
        {
            path.push_back(i);
            dfs(path,i+1,n,k-1);//递归到i+1，且需要的数-1(k--)
            path.pop_back();//回溯时恢复现场。
        }
    }
};
```

---

## LT[257. 二叉树的所有路径](https://leetcode-cn.com/problems/binary-tree-paths/)

题目描述：

给定一个二叉树，返回所有从根节点到叶子节点的路径。

**说明:** 叶子节点是指没有子节点的节点。

```C++
示例:

输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]

解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
```

  	

```C++
Code:
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution
{
public:
    vector<string> ans;
    vector<string> binaryTreePaths(TreeNode *root)
    {
        string path;
        dfs(root, path);
        return ans;
    }
    void dfs(TreeNode *root, string path)
    {
        if (!root)
            return;
        if (path.size())    path += "->";
        path += to_string(root->val);
        TreeNode *left = root->left;
        TreeNode *right = root->right;

        if (!left && !right)
        {
            ans.push_back(path);
        }
        else
        {
            dfs(left, path);
            dfs(right, path);
        }
    }
};
```



---

## LT [93. 复原IP地址](https://leetcode-cn.com/problems/restore-ip-addresses/)



题目描述：

给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。

有效的 IP 地址 正好由四个整数（每个整数位于 0 到 255 之间组成，且不能含有前导 0），整数之间用 '.' 分隔。

例如："0.1.2.201" 和 "192.168.1.1" 是 有效的 IP 地址，但是 "0.011.255.245"、"192.168.1.312" 和 "192.168@1.1" 是 无效的 IP 地址。

 ```c++
示例 1：

输入：s = "25525511135"
输出：["255.255.11.135","255.255.111.35"]
示例 2：

输入：s = "0000"
输出：["0.0.0.0"]
示例 3：

输入：s = "1111"
输出：["1.1.1.1"]
示例 4：

输入：s = "010010"
输出：["0.10.0.10","0.100.1.0"]
示例 5：

输入：s = "101023"
输出：["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]

 ```

```c++
Code : class Solution
{
public:
    vector<string> ans;//记录答案
    vector<string> restoreIpAddresses(string s)
    {
        string path;//过程
        dfs(s, 0, 0, path);
        return ans;
    }
    void dfs(string &s, int u, int k, string path)
        //s:字符数组S，u:当前在s的位置，k为限制数(ip只可以有4位)path记录过程变量
    {
        if (u == s.size())//递归基
        {
            if (k == 4)//当ip的为四位数时，存入一个答案。
                ans.push_back(path.substr(1));//
            //substr(1)从下标为1返回字符串
            return;
        }
        if (k > 4)//剪枝,没必要做多余的操作。
            return;

        if (s[u] == '0')//如果是0，他只能单独成为四个数中的一个数。
        {
            path += ".0";
            dfs(s, u + 1, k + 1, path);
        }
        else
        {
            for (int i = u, t = 0; i < s.size(); i++)//t为ip地址中要求的一个数
            {
                t = t * 10 + (s[i] - '0');//2*10 +5 -> 25*10 +5 -> 255(例子)
                if (t < 256)
                {
                    dfs(s, i + 1, k + 1, path + '.' + to_string(t));
                }
                else//t的增长是单调递增的，一旦大于256，便不可挽回,所以直接break。
                    break;
            }
        }
    }
};
```

解题思路:

DFS

## LT[95. 不同的二叉搜索树 II](https://leetcode-cn.com/problems/unique-binary-search-trees-ii/)

**题目描述:**

给定一个整数 *n*，生成所有由 1 ... *n* 为节点所组成的 二叉搜索树 (BST)。

```c++
输入：3
输出：
[
  [1,null,3,2], 
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释：
以上的输出对应以下 5 种不同结构的二叉搜索树：

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
 
提示：
0 <= n <= 8
```



 ```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution
{
public:
    vector<TreeNode *> generateTrees(int n)
    {
        if (!n)//没有节点的情况，返回空树。
            return vector<TreeNode *>();
        return dfs(1, n);
    }
    
    vector<TreeNode *> dfs(int l, int r)
    {
        vector<TreeNode *> res;
        if (l > r)//如果区间不存在元素，返回NULL。
        {
            res.push_back(NULL);//NULL也是一种子树
            return res;
        }
        for (int i = l; i <= r; i++)
        {
            auto left = dfs(l, i - 1), right = dfs(i + 1, r);//i为根树。[l,i-1]左子树，[i+1,r]右子树。
            for (auto &lt : left)//将左右子树组合，根节点为i
                for (auto &rt : right)
                {

                    auto root = new TreeNode(i);		
                    root->left = lt;
                    root->right = rt;
                    res.push_back(root);
                }
        }
        return res;
    }
};
 ```

## LT[394. 字符串解码](https://leetcode-cn.com/problems/decode-string/)

**题目描述:**

给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

```c++
示例 1：

输入：s = "3[a]2[bc]"
输出："aaabcbc"
示例 2：

输入：s = "3[a2[c]]"
输出："accaccacc"
示例 3：

输入：s = "2[abc]3[cd]ef"
输出："abcabccdcdcdef"
示例 4：

输入：s = "abc3[cd]xyz"
输出："abccdcdcdxyz"

```

解题思路：

k是可以嵌套，比如：2[ 2[a]bb] ->ans : aabbaabb

整个过程对应一个DFS搜索树，当遇到`"["`向下递归一层,遇到`" ] "`,向上递归一层。这道题，需要处理的细节不少，尤其是边界问题

````c++
class Solution {
public:
    
    string decodeString(string s) {
        string res;//不要存成全局变量，因为递归求res，每个递归层的res都是不同的。
        for(int i=0;i<s.size(); )
        {	//isdigit是c++中比较冷门的函数，作用也很简单就是判断一个字符是不是数字
            if(!isdigit(s[i]))res+=s[i++];
            else 
            {
                int k=0;//用来存储[前的数字的
                while(isdigit(s[i]))k=k*10 +s[i++]-'0';
                int j=i+1,sum=1;//此时i指向当前第一个'['，j的位置可想而知。
                //整个递归过程类似括号匹配，遇到`[`sum++，遇到`]`sum--，当sum=0时，j指向`]`的下一位
                while(sum>0)
                {
                    if(s[j]=='[')sum++;
                    if(s[j]==']')sum--;
                    j++;
                }//注意`j`最后指向`]`下一位。
                string r=decodeString(s.substr(i+1,j-i-2));
                //之后递归`[]`内的字符。
                //`i`指向`[`，i+1，可想而知。那么右边界呢。举个例子具体计算。
                while(k--)res+=r;
                i=j;//重置i的位置
            }
        }
        return res;
    }
   
};
````

## LT[341. 扁平化嵌套列表迭代器](https://leetcode-cn.com/problems/flatten-nested-list-iterator/)

**题目描述：**

**给你一个嵌套的整型列表。请你设计一个迭代器，使其能够遍历这个整型列表中的所有整数。**

**列表中的每一项或者为一个整数，或者是另一个列表。其中列表的元素也可能是整数或是其他列表。**

```
示例 1:

输入: [[1,1],2,[1,1]]
输出: [1,1,2,1,1]
解释: 通过重复调用 next 直到 hasNext 返回 false，next 返回的元素的顺序应该是: [1,1,2,1,1]。
示例 2:

输入: [1,[4,[6]]]
输出: [1,4,6]
解释: 通过重复调用 next 直到 hasNext 返回 false，next 返回的元素的顺序应该是: [1,4,6]。

```

解题思路:递归求解[]内部序列。

int next()函数返回列表下一个值

int hasNext()返回下一个值是否存在

```c++
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds, if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Return the nested list that this NestedInteger holds, if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */
//int getInteger() const; 当[]中只有一个数的时候就返回
//bool isInteger() const;  当[]内为一个整数时，返回TRUE
//void getList()  获取[]内的列表
class NestedIterator {
public:
    int cnt=0;
    vector<int> ans;
    NestedIterator(vector<NestedInteger> &nestedList) {
        dfs(nestedList);
        
    }
    void dfs(vector<NestedInteger> &nestedList)
    {
        for(auto &x :nestedList)
        {
            if(x.isInteger())ans.push_back(x.getInteger());
            else dfs(x.getList());
        }
    }
    int next() {
        return ans[cnt++];
    }
    
    bool hasNext() {
        return cnt<ans.size();
    }
};

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i(nestedList);
 * while (i.hasNext()) cout << i.next();
 */
```

## LT[756. Pyramid Transition Matrix](https://leetcode-cn.com/problems/pyramid-transition-matrix/)

**题目描述：现在，我们用一些方块来堆砌一个金字塔。 每个方块用仅包含一个字母的字符串表示。**

**使用三元组表示金字塔的堆砌规则如下：**

**对于三元组(A, B, C) ，“C”为顶层方块，方块“A”、“B”分别作为方块“C”下一层的的左、右子块。当且仅当(A, B, C)是被允许的三元组，我们才可以将其堆砌上。**

**初始时，给定金字塔的基层 bottom，用一个字符串表示。一个允许的三元组列表 allowed，每个三元组用一个长度为 3 的字符串表示。**

**如果可以由基层一直堆到塔尖就返回 true ，否则返回 false 。**

```c++
输入：bottom = "BCD", allowed = ["BCG", "CDE", "GEA", "FFF"]
输出：true
解析：
可以堆砌成这样的金字塔:
    A
   / \
  G   E
 / \ / \
B   C   D

因为符合('B', 'C', 'G'), ('C', 'D', 'E') 和 ('G', 'E', 'A') 三种规则。
示例 2：

输入：bottom = "AABA", allowed = ["AAA", "AAB", "ABA", "ABB", "BAC"]
输出：false
解析：
无法一直堆到塔尖。
注意, 允许存在像 (A, B, C) 和 (A, B, D) 这样的三元组，其中 C != D。
 

提示：

bottom 的长度范围在 [2, 8]。//bottom的范围很短，直接暴力dfs
allowed 的长度范围在[0, 200]。
方块的标记字母范围为{'A', 'B', 'C', 'D', 'E', 'F', 'G'}。
```



```c++
code:
class Solution {
public:
    vector<char>allows[7][7];//数组长度取决于方块字母范围{'A', 'B', 'C', 'D', 'E', 'F', 'G'}。 
    //allows 的下标是allowed的左右子层，allowed的key是顶层
    bool pyramidTransition(string bottom, vector<string>& allowed) {
            for(auto allow:allowed)
            {
                int a=allow[0]-'A',b=allow[1]-'A',c=allow[2];
                allows[a][b].push_back(c);
            }
        return dfs(bottom,"");//初始状态下一层为bottom，当前层为""(空)
    }
    bool dfs(string &last,string now)//last为上一层元素，now为当前层。
    {
        int a=last[now.size()]-'A',b=last[now.size()+1]-'A';
        //a，b分别为底层的左右子树。
        if(last.size()==1)return true;//递归基
        
        if(last.size()==now.size()+1)return dfs(now,"");//开始递归下一层
        
        for(auto c:allows[a][b])//AAA,AAB出现左右子树有两个top的情况
        {
            if(dfs(last,now+c))
                return true;
        }
        return false;
    }
};
```

题解思路：

dfs

## LT[79. 单词搜索](https://leetcode-cn.com/problems/word-search/)

题目：

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

```c++
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true
给定 word = "SEE", 返回 true
给定 word = "ABCB", 返回 false
 

```

```c++
class Solution {
public:
    bool st[210][210]={0};//
    int n,m;
    vector<vector<char>>_board;
    string _word;
    bool exist(vector<vector<char>>& board, string word) {
        n=board.size();
        m=board[0].size();
        _board=board;
        _word=word;
        for(int i=0;i<n;i++)
            for(int j=0;j<m;j++)
            {
                if(word[0]==board[i][j])//找开头字母
                {
                    if(dfs(i,j,1))
                    return true;
                }
            }
        return false;
    }
    bool dfs(int x,int y,int u)//i，j代表字母在board的位置，u代表第几个字母
    {
        if(u==_word.size())return  true;//递归基
        int dx[4]={0,1,-1,0},dy[4]={1,0,0,-1};
        st[x][y]=true;//
        for(int i=0;i<4;i++)
        {
            int a=dx[i]+x,b=dy[i]+y;
            if(a>=0&&a<n&&b>=0&&b<m&&!st[a][b]&&_board[a][b]==_word[u])
            {
                if(dfs(a,b,u+1))return true;
            }
        }
        st[x][y]=false;//复原现场
        return false;
    }
        
};
```

