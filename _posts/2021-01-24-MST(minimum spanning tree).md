---
title: "MST(minimum spanning tree)"
date: 2021-01-24 04:56:00 +0900
categories:
- algorithm
tags:
- MST
---

<!-- more -->

```c++
#include <bits/stdc++.h>
#define pii pair<int,int>
using namespace std;

struct element
{
	int u,v,w;
};

bool operator<(element a,element b)
{
    return a.w>b.w;
}

vector<pii> tree[10001];
int u[10001];
priority_queue<element> pq;

int find(int a)
{
    if(u[a]<0)return a;
    return u[a]=find(u[a]);
}

bool merge(int a,int b)
{
    a=find(a),b=find(b);
    if(a==b)return false;
    if(-u[a]<-u[b])swap(a,b);
    u[a]+=u[b],u[b]=a;
    return true;
}

//v: 정점의 개수. main 에서 pq에 간선 넣고, u배열 -1로 초기화. mst의 가중치 리턴.
int mst(int v)
{
    int weight=0;
    while (!pq.empty())
    {
        element e=pq.top();
        pq.pop();
        if(merge(e.u,e.v))
        {
            weight+=e.w;
            tree[e.u].push_back({e.v,e.w});
            tree[e.v].push_back({e.u,e.w});
        }
    }
    return weight;
}

int main()
{
	int v,e;
	scanf("%d %d",&v,&e);
	while(e--)
	{
	    int a,b,c;
		scanf("%d %d %d",&a,&b,&c);
		pq.push({a,b,c});
	}
	fill(u+1,u+1+v,-1);
	printf("%d",mst(v));
	return 0;
}
```



# 관련문제

[백준1197 : 최소 스패닝 트리](https://www.acmicpc.net/problem/1197)