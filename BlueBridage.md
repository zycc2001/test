### [\93. 递归实现组合型枚举](https://www.acwing.com/problem/content/95/)

```c++
#include<iostream>
using namespace std;
int n,m;
const int N=30;
bool used[N];//判断是否被用过
int way[N];//存结果
void dfs(int u,int start)//u为第几位，start保证大于前一位的一个数
{
    if(u+n-strat)return;//剪枝 如果后面的数不够填上位数，直接返回。
    if(u>m)
    {
        for(int i=1;i<=m;i++)printf("%d ",way[i]);
        puts("");
        return ;
    }
    for(int i=start;i<=n;i++)
    {
        if(!used[i])
        {
            way[u]=i;
            used[i]=true;
            dfs(u+1,i+1);
            used[i]=false;
            way[u]=0;
        }
        
    }
}
int main()
{
    cin>>n>>m;
    dfs(1,1);
}//画出递归搜索树
```

![image-20201028133007332](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20201028133007332.png)



### \ 92. [递归实现指数型枚举](https://www.acwing.com/problem/content/94/)

```c++
#include<iostream>
using namespace std;

const int N=16;
int st[N];//存结果
int n;

void dfs(int u)
{
    if(u==n)
    {
        for(int i=0;i<n;i++)
        {
            if(st[i])printf("%d ",i+1);
        }
        puts("");
        return ;
    }
    st[u]=1;//选的情况
    dfs(u+1);
    st[u]=0;//回溯恢复
    
    dfs(u+1);//不选的情况
}

int main()
{
    cin>>n;
    dfs(0);
}	

```



![image-20201028133127665](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20201028133127665.png)

### [\94. 递归实现排列型枚举](https://www.acwing.com/problem/content/96/)

```c++
#include<iostream>
#include<cstring>
using namespace std;

const int N=10;
int st[N];
bool used[N];//该数是否被用过
int n;

void dfs(int u)
{
    if(u==n)
    {
        for(int i=0;i<n;i++)
        {
            printf("%d ",st[i]);
        }
        puts("");
        return ;
    }
    for(int i=0;i<n;i++)
        if(!used[i])
        {
            st[u]=i+1;
            used[i]=true;
            dfs(u+1);

            used[i]=false;
            st[u]=0;
        }
}

int main()
{
    cin>>n;
    dfs(0);
}

```

![image-20201028133258457](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20201028133258457.png)

### [\1209. 带分数](https://www.acwing.com/problem/content/1211/)