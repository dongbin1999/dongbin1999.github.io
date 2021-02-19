---
title: "union-find"
date: 2021-01-24 04:32:00
categories:
- algorithm
tags:
- union-find
---

<!-- more -->

# 분리 집합

```c++
#include <bits/stdc++.h>
using namespace std;

//처음에 u 배열 -1로 초기화.
int u[1000001];

int find(int a)
{
    if(u[a]<0)return a;
    return u[a]=find(u[a]);
}

bool merge(int a,int b)
{
    a=find(a),b=find(b);
    if(a==b)return false;
    //union by rank. path compression을 하지 않을 때 사용.
    //if(-u[a]<-u[b])swap(a,b);
    u[a]+=u[b],u[b]=a;
    return true;
}

int main(void)
{
    int n,m;
    scanf("%d %d",&n,&m);
    fill(u,u+1+n,-1);
    while(m--)
    {
        int c,a,b;
        scanf("%d %d %d",&c,&a,&b);
        if(c) printf(find(a)==find(b)?"YES\n":"NO\n");
        else merge(a,b);
    }
    return 0;
}
```

## 시간복잡도

$O(Mlog*N) \approx O(M)$

> N : 정점 수, M : find 연산 수행 횟수



## 관련문제

[백준1717 : 집합의 표현](https://www.acmicpc.net/problem/1717)