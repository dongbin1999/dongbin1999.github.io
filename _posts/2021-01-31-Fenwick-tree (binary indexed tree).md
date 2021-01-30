---
title: "Fenwick-tree (binary indexed tree)"
date: 2021-01-31 03:05:00 +0900
categories:
- data structure
tags:
- Fenwick-tree
---

<!-- more -->

```c++
#include <bits/stdc++.h>
#define ll long long
using namespace std;
//크기는 n=sz.
const int sz=1000000;
ll BIT[sz+1];
ll arr[sz+1];

//sum(i) : 1번째~i번째 수의 총합
ll sum(int i)
{
    ll ret=0;
    while(i>0)
    {
        ret+=BIT[i];
        i-=i&-i;
    }
    return ret;
}

void update(int i, ll diff)
{
    while(i<=sz)
    {
        BIT[i]+=diff;
        i+=i&-i;
    }
}

int main(void)
{
    int n,m,k;
    scanf("%d %d %d",&n,&m,&k);

    for(int i=1;i<=n;i++)
    {
        scanf("%lld",&arr[i]);
        update(i,arr[i]);
    }

    int q=m+k;
    while(q--)
    {
        int a; scanf("%d",&a);
        if(a==1)
        {
            int b;ll c; scanf("%d %lld",&b,&c);
            update(b,c-arr[b]);
            arr[b]=c;
        }
        else
        {
            int l,r; scanf("%d %d",&l,&r);
            printf("%lld\n",sum(r)-sum(l-1));
        }
    }
    return 0;
}
```



# 관련문제

[백준2042 : 구간 합 구하기](https://www.acmicpc.net/problem/2042)