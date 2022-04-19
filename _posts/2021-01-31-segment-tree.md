---
title: segment-tree
date: {}
categories:
  - data structure
tags:
  - segment-tree
published: true
---

<!-- more -->

# 세그먼트 트리

```c++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
//크기는 n<sz 이면서 sz=1<<k 꼴로. 2^17=131072 / 2^18=262144 / 2^19=524288 / 2^20=1048576
//고쳐야 할 부분 (1)~(5)
const int sz=1<<20;
ll arr[sz*2];

//처음 값 입력받은 후 트리 구축.
void construct(){
    for(int i=sz-1;i>=1;i--)
        arr[i]=arr[i*2]+arr[i*2+1];//(1)
}

void update(int i,ll val){
    i+=sz,arr[i]=val;
    while(i>1)i/=2,arr[i]=arr[i*2]+arr[i*2+1];//(2)
}

ll query(int s,int e,int node,int ns,int ne){
    if(e<ns||ne<s)return 0;//(3)
    if(s<=ns&&ne<=e)return arr[node];//(4)
    int mid=(ns+ne)/2;
    return query(s,e,node*2,ns,mid)+query(s,e,node*2+1,mid+1,ne);//(5)
}

int main(){
    int n,m,k;
    scanf("%d %d %d",&n,&m,&k);

    //값 입력받는 위치 주의.(+sz)
    for(int i=1;i<=n;i++)
        scanf("%lld",&arr[i+sz]);
    construct();

    int q=m+k;
    while(q--){
        int a; scanf("%d",&a);
        if(a==1){
            int b;ll c; scanf("%d %lld",&b,&c);
            update(b,c);
        }
        else{
            int l,r; scanf("%d %d",&l, &r);
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

[백준2042 : 구간 합 구하기](https://www.acmicpc.net/problem/2042)
