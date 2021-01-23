---
title: "Floyd-Warshall"
date: 2021-01-24 04:15:00 +0900
categories:
- algorithm
tags:
- Floyd-Warshall
---

<!-- more -->

```c++
#include <bits/stdc++.h>
using namespace std;

//간선 입력 전에, adj 배열 1e9로 초기화.
int adj[101][101];
void floyd_warshall(int n)
{
    for(int via=1;via<=n;via++)
        for(int s=1;s<=n;s++)
            for(int e=1;e<=n;e++)
                if(s!=e)
                    adj[s][e]=min(adj[s][e],adj[s][via]+adj[via][e]);

    //출력. adj[i][j] : i->j에 필요한 최소 비용.
    for(int i=1;i<=n;i++)
    {
        for(int j=1;j<=n;j++)
            printf("%d ",adj[i][j]==1e9?0:adj[i][j]);
        printf("\n");
    }
}

int main()
{
    int n,m;
    scanf("%d %d",&n,&m);
    for(int i=1;i<=n;i++)
        fill(adj[i]+1,adj[i]+1+n,1e9);
    while(m--)
    {
        int a,b,c;
        scanf("%d %d %d",&a,&b,&c);
        adj[a][b]=min(adj[a][b],c);
    }
    floyd_warshall(n);
    return 0;
}
```



# 관련문제

[백준11404 : 플로이드](https://www.acmicpc.net/problem/11404)

