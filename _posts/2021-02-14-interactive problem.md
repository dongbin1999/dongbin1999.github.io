---
title: "interactive problem"
date: 2021-02-14 18:53:00 +0900
categories:
- PS
tags:
- codeforces
- interactive
---

<!-- more -->

# 문제

[Codeforces 1425F - Flamingoes of Mystery](https://codeforces.com/problemset/problem/1425/F)

1. $N$ 개의 신비한 새장이 있고, $i$ 번째 새장에는 $A_i$ 마리의 플라밍고가 들어있습니다.
2. `? L R` 의 형태로 질문을 하면, $L$ ~ $R$ 번째 새장에 들어있는 플라밍고의 마릿수 합을 알려줍니다.
3. 최대 $N$ 번의 질문으로, 각 새장에 들어있는 플라밍고의 수를 알아내야 합니다.

```c++
#include <bits/stdc++.h>
using namespace std;

int sum[1001],ans[1001];

int main()
{
    int n; scanf("%d",&n);
    for(int i=2;i<=n;i++)
    {
        printf("? 1 %d\n",i);
        fflush(stdout);
        scanf("%d",&sum[i]);
    }

    printf("? 2 3\n");
    fflush(stdout);
    int tt; scanf("%d",&tt);

    ans[1]=sum[1]=sum[3]-tt;
    for(int i=2;i<=n;i++)
        ans[i]=sum[i]-sum[i-1];

    printf("! ");
    for(int i=1;i<=n;i++)
        printf("%d ",ans[i]);
    return 0;
}
```

## 입력

```c++
6

5

9

15

22

30

8

```

## 출력

```c++

? 1 2

? 1 3

? 1 4

? 1 5

? 1 6

? 2 3

! 1 4 4 6 7 8
```
