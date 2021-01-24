---
title: "SCC(strongly connected component)"
date: 2021-01-24 18:10:00 +0900
categories:
- algorithm
tags:
- SCC
---

<!-- more -->

```c++
#include <bits/stdc++.h>
using namespace std;
const int sz=100001;
//sz : n+1로 설정.
int dfsn[sz],scc[sz],dfsnumber,sccnumber;
//graph : 처음 주어지는 그래프 / dag : SCC로 묶인 그래프 / group[i] : i번 scc 노드에 묶여있는 정점들.
vector<int> graph[sz],dag[sz],group[sz];
stack<int> s;
int indegree[sz];

//타잔 알고리즘 이용.(scc 결과의 역순이 위상정렬한 dag 의 결과와 같음.)
int SCC(int node)
{
    dfsn[node]=++dfsnumber;
    s.push(node);
    int topmost=dfsn[node];
    for(int to:graph[node])
        if(!dfsn[to]) topmost=min(topmost, SCC(to));
        else if(!scc[to]) topmost=min(topmost,dfsn[to]);

    if(topmost==dfsn[node])
    {
        ++sccnumber;
        while(true)
        {
            int t=s.top();
            s.pop();
            scc[t]=sccnumber;
            group[sccnumber].push_back(t);
            if(t==node) break;
        }
    }
    return topmost;
}

void init(int n)
{
    dfsnumber=0,sccnumber=0;
    for(int i=1;i<=n;i++)
        graph[i].clear(),dag[i].clear(),dfsn[i]=0,indegree[i]=0,scc[i]=0,group[i].clear();
}

int main(void)
{
    int tc;
    scanf("%d",&tc);
    while(tc--)
    {
        int n,m;
        scanf("%d %d", &n,&m);
        while(m--)
        {
            int x,y;
            scanf("%d %d",&x,&y);
            graph[x].push_back(y);
        }
        for(int i=1;i<=n;i++)
            if(!dfsn[i]) SCC(i);

        //이제 위상정렬이 가능해짐.
        for(int node=1;node<=n;node++)
            for(int to:graph[node])
                if(scc[node]!=scc[to])
                {
                    dag[scc[node]].push_back(scc[to]);
                    indegree[scc[to]]++;
                }

        int ans=0;
        for(int i=1;i<=sccnumber;i++)
            if (!indegree[i]) ans++;
        printf("%d\n",ans);
        init(n);
    }
    return 0;
}
```



# 관련문제

[백준4196 : 도미노](https://www.acmicpc.net/problem/4196)