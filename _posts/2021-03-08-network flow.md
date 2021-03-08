---
title: "network flow"
date: 2021-03-08 19:08:00
categories:
- algorithm
tags:
- network flow
---

<!-- more -->

# 최대 유량

```c++
#include <bits/stdc++.h>
using namespace std;

//크기는 모든 정점 개수의 합+1 (소스 S=0,싱크 E=n+m+1)
int cap[402][402], flow[402][402];
vector<int> graph[402];

int main()
{
    int n,m;scanf("%d %d",&n,&m);
    int S=0,E=n+m+1;

    for(int i=1;i<=n;i++)
    {
        int q,s;scanf("%d",&q);
        while(q--)
        {
            scanf("%d",&s);
            cap[i][s+n]=1;
            graph[i].push_back(s+n);
            graph[s+n].push_back(i);
        }
    }

    //각 번호당 소는 한 마리임.(소스->)
    for(int i=1;i<=n;i++)
    {
        cap[S][i]=1;
        graph[S].push_back(i);
        graph[i].push_back(S);
    }

    //축사 한 칸에는 최대 한 마리의 소만 들어감.(->싱크)
    for(int i=n+1;i<=m+n;i++)
    {
        cap[i][E]=1;
        graph[i].push_back(E);
        graph[E].push_back(i);
    }

    int ans=0;
    //Edmonds-Karp 알고리즘.
    while(true)
    {
        vector<int>prev(402,-1);
        queue<int> q; q.push(S);
        while(!q.empty()&&prev[E]==-1)
        {
            int cur=q.front();q.pop();
            for(int go:graph[cur])
                if(cap[cur][go]-flow[cur][go]>0&&prev[go]==-1)
                {
                    prev[go]=cur, q.push(go);
                    if(go==E) break;
                }
        }
        if(prev[E]==-1) break;
        int mn=1e9, cur=E;
        while(cur!=S)
        {
            mn=min(mn,cap[prev[cur]][cur]-flow[prev[cur]][cur]);
            cur=prev[cur];
        }
        cur=E;
        while(cur!=S)
        {
            flow[prev[cur]][cur]+=mn;
            flow[cur][prev[cur]]-=mn;
            cur=prev[cur];
        }
        ans+=mn;
    }
    printf("%d",ans);
    return 0;
}
```

## 시간복잡도

$min(O(E^{2}V),O(EF) \approx O(E^{2}V)$

> V : 정점 수, E : 간선 수, F : 답으로 출력하는 수



## 관련문제

[백준2188 : 축사 배정](https://www.acmicpc.net/problem/2188)