---
title: "Bellman-Ford"
date: 2021-01-24 03:54:00 +0900
categories:
- algorithm
tags:
- Bellman-Ford
---

<!-- more -->

```c++
#include <bits/stdc++.h>
#define ll long long
#define pil pair<int,ll>
using namespace std;

ll dist[501];
vector<pil> graph[501];

//음의 사이클이 발생하면 false 리턴. n:정점 개수.
bool bellman_ford(int n)
{
    fill(dist+1,dist+1+n,1e18); dist[1] = 0;
    int loop=n-1;
    while(loop--)
        for(int s=1;s<=n;s++)
            for(pil go:graph[s])
                if(dist[s]!=1e18)
                    dist[go.first]=min(dist[go.first],dist[s]+go.second);

    //한번더 돌아서 값이 갱신되면, 음의 사이클이 존재하는 것.
    for(int s=1;s<=n;s++)
        for(pil go:graph[s])
            if(dist[go.first]>dist[s]+go.second&&dist[go.first]!=1e18)
                return false;

    for(int i=2;i<=n;i++)
        printf("%lld\n",dist[i]==1e18?-1ll:dist[i]);
    return true;
}

int main()
{
    int n,m;
    scanf("%d %d",&n,&m);
    while(m--)
    {
        int a,b;ll c;
        scanf("%d %d %lld",&a,&b,&c);
        graph[a].push_back({b,c});
    }
    bool ok=bellman_ford(n);
    if(!ok) printf("-1");
    return 0;
}
```



# 관련문제

[백준11657 : 타임머신](https://www.acmicpc.net/problem/11657)

