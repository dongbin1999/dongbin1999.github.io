---
title: "LCA(lowest common ancestor)"
date: 2021-01-24 16:51:00 +0900
categories:
- algorithm
tags:
- LCA
---

<!-- more -->

```c++
#include <bits/stdc++.h>
using namespace std;
const int sz=17;
//(1<<sz)>=n이 되게 관리.
vector<int> tree[1<<sz];
int depth[1<<sz];//depth[i] : i번 노드의 깊이(루트노드에서부터의 거리)
int sparse[1<<sz][sz];//sparse[i][j] : i번째 노드의 2^j번째 부모. 1번(루트)노드의 부모도 1이라고 가정.

void go(int node,int d,int parent)
{
    sparse[node][0]=parent;
    depth[node]=d;
    //어떤 노드의 2^i번째 부모는, 그 노드의 2^(i-1)번째 부모의 2^(i-1)번째 부모임.
    for(int i=1;i<sz;i++)
        sparse[node][i]=sparse[sparse[node][i-1]][i-1];
    for(int to:tree[node])
        if(parent!=to)
            go(to,d+1,node);
}

int LCA(int a,int b)
{
    if(depth[a]>depth[b])
        swap(a,b);//b가 더 깊은 점.
    for(int i=sz-1;i>=0;i--)//b를 a 높이까지 올려줌.
        if(depth[sparse[b][i]]>=depth[a])
            b=sparse[b][i];
    if(a==b)return a;//a,b가 같은 점이면 그 점이 LCA.
    for(int i=sz-1;i>=0;i--)
        if(sparse[a][i]!=sparse[b][i])
            a=sparse[a][i],b=sparse[b][i];
    return sparse[a][0];//a,b의 한단계 위가 LCA.
}

int main()
{
    int n,m;
    scanf("%d", &n);
    for(int i=1;i<n;i++)
    {
        int a,b;
        scanf("%d %d",&a,&b);
        tree[a].push_back(b);
        tree[b].push_back(a);
    }
    go(1,0,1);
    scanf("%d",&m);
    while(m--)
    {
        int a,b;
        scanf("%d %d",&a,&b);
        printf("%d\n",LCA(a,b));
    }
    return 0;
}
```



# 관련문제

[백준11438 : LCA 2](https://www.acmicpc.net/problem/11438)