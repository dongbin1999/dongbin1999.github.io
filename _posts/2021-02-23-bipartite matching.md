---
title: "bipartite matching"
date: 2021-02-23 16:50:00
categories:
- algorithm
tags:
- bipartite matching
---

<!-- more -->

# 이분 매칭

```c++
#include <bits/stdc++.h>
using namespace std;

//a,b의 크기는 이분 그래프 각각의 정점 수. vis,graph의 크기는 a의 크기와 같게.
int a[1001],b[1001];
bool vis[1001];
vector<int> graph[1001];

bool BM(int cur)
{
    vis[cur]=true;
    for(int go:graph[cur])
        if(b[go]==-1||!vis[b[go]]&&BM(b[go]))
        {
            a[cur]=go;
            b[go]=cur;
            return true;
        }
    return false;
}

int main()
{
    int n,m;scanf("%d %d",&n,&m);
    //아직 매칭되기 전.(-1)
    fill(a+1,a+1+n,-1);
    fill(b+1,b+1+m,-1);

    for(int i=1;i<=n;i++)
    {
        int work,t;scanf("%d",&work);
        while(work--)
        {
            scanf("%d",&t);
            graph[i].push_back(t);
        }
    }

    int ans=0;
    for(int i=1;i<=n;i++)
    {
        fill(vis+1,vis+1+n,false);
        if(BM(i)) ans++;//새로운 매칭에 성공.
    }
    printf("%d",ans);
    return 0;
}
```

## 시간복잡도

$O(VE)$

> V : 정점 수, E : 간선 수



## 관련문제

[백준11375 : 열혈강호](https://www.acmicpc.net/problem/11375)