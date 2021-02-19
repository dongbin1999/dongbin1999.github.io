---
title: "segment-tree (with lazy propagation)"
date: 2021-01-31 02:40:00
categories:
- data structure
tags:
- segment-tree (with lazy propagation)
---

<!-- more -->

# 세그먼트 트리 (구간 업데이트)

```c++
#include <bits/stdc++.h>
#define ll long long
using namespace std;
//크기는 n<sz 이면서 sz=1<<k 꼴로. 2^17=131072 / 2^18=262144 / 2^19=524288 / 2^20=1048576
//고쳐야 할 부분 (1)~(11)
const int sz = 1<<20;
ll arr[sz*2], lazy[sz*2];

//처음 값 입력받은 후 트리 구축.
void construct()
{
    for(int i=sz-1;i>=1;i--)
        arr[i]=arr[i*2]+arr[i*2+1];//(1)
}

//lazy 적용.
void propagate(int node,int ns,int ne)
{
    if(!lazy[node]) return;//(2)
    if(node<sz)
    {
        lazy[node*2]+=lazy[node];//(3)
        lazy[node*2+1]+=lazy[node];//(4)
    }
    arr[node]+=lazy[node]*(ll)(ne-ns+1);//(5)
    lazy[node]=0LL;//(6)
}

void update(int s,int e,ll k,int node,int ns,int ne)
{
    propagate(node,ns,ne);
    if(e<ns||ne<s)return;
    if (s<=ns&&ne<=e)
    {
        lazy[node]+=k;//(7)
        propagate(node,ns,ne); return;
    }
    int mid=(ns+ne)/2;
    update(s,e,k,node*2,ns,mid),update(s,e,k,node*2+1,mid+1,ne);
    arr[node]=arr[node*2]+arr[node*2+1];//(8)
}

ll query(int s,int e,int node,int ns,int ne)
{
    propagate(node,ns,ne);
    if(e<ns||ne<s)return 0;//(9)
    if(s<=ns&&ne<=e)return arr[node];//(10)
    int mid=(ns+ne)/2;
    return query(s,e,node*2,ns,mid)+query(s,e,node*2+1,mid+1,ne);//(11)
}

int main(void)
{
    int n,m,k;
    scanf("%d %d %d",&n,&m,&k);

    //값 입력받는 위치 주의.(+sz)
    for(int i=1;i<=n;i++)
        scanf("%lld",&arr[i+sz]);
    construct();

    int q=m+k;
    while(q--)
    {
        int a; scanf("%d",&a);
        if(a==1)
        {
            int l,r;ll d; scanf("%d %d %lld",&l,&r,&d);
            update(l,r,d,1,0,sz-1);
        }
        else
        {
            int l,r; scanf("%d %d",&l,&r);
            printf("%lld\n", query(l,r,1,0,sz-1));
        }
    }
    return 0;
}
```

## 시간복잡도

* 전처리 : $O(N)$
* 구간 합 구하기 : $O(logN)$
* 값 업데이트 : $O(logN)$

> N : 수의 개수



## 관련문제

[백준10999 : 구간 합 구하기 2](https://www.acmicpc.net/problem/10999)