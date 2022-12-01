---
title: "topological-sort"
date: 2021-01-24 16:31:00
categories:
- algorithm
tags:
- topological-sort
---

<!-- more -->

# 위상 정렬

```c++
#include <bits/stdc++.h>
using namespace std;

//간선 추가할때 indegree 관리.
vector<int> dag[32001];
int indegree[32001];
//n은 정점 수.
void topological_sort(int n)
{
    vector<int> ans;//위상정렬된 정점.
    queue<int> q;
    for(int i=1;i<=n;i++)
        if(!indegree[i])
            q.push(i);
    while(!q.empty())
    {
        int t=q.front();
        q.pop();
        for(int go:dag[t])
            if(--indegree[go]==0)
                q.push(go);
        ans.push_back(t);
    }
    for(int i:ans)
        printf("%d ",i); //출력.
}

int main()
{
    int n,m;
    scanf("%d %d",&n,&m);
    while(m--)
    {
        int a,b;
        scanf("%d %d",&a,&b);
        dag[a].push_back(b);
        indegree[b]++;
    }
    topological_sort(n);
    return 0;
}
```

## 시간복잡도

$O(V+E)$

> V : 정점 수, E : 간선 수



## 관련문제

[백준2252 : 줄 세우기](https://www.acmicpc.net/problem/2252)