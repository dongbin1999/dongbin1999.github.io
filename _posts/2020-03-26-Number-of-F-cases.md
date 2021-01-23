---
title: "Number of F cases"
date: 2020-03-26 16:27:40 +0900
categories:
- university
tags:
- assignment
---

.

<h1>F를 받게되는 경우의 수</h1>

<h5>201901694 이동빈</h5>

> 총 수업시간 15*3 = 45시간 중, 15시간 이상 결석하면 F를 받게 된다.



**가정)** 

1. 출결체크는 매 수업시간 정각마다 이루어진다고 가정했습니다. (분 단위로 나누면 경우의 수가 너무 많음.)
2. 공결, ~~출튀~~, 수업 도중에 나갔다 들어오는 것과 같은 특수한 경우는 고려하진 않았습니다. (같은 이유.)



---

__45시간 중 15시간, 16시간, ... , 45시간을 결석하면 F를 받게 되므로, 경우의 수는 다음과 같습니다.__

$$
\displaystyle\sum_{i=15}^{45}\binom{45}{i} = \displaystyle\sum_{i=15}^{45}\frac{45!}{i!(45-i)!} = _{45}C_{15} + _{45}C_{16} + ... + _{45}C_{45}
$$
_(계산 과정에서 45!의 값이 long long 범위를 넘어가서, 다른 방법으로 계산했습니다.)_

___



<h4>Java</h4>

```java
public class homework {
    public static void main (String []args)
    {
        long answer = 0;
        long combination = 1;
        for(long b = 45, c = 1; c <= 45; b--, c++)
        {
            combination = (combination * b) / c;
            if(c >= 15)
            {
                answer += combination;
                System.out.println("45 C " + c + " = " + combination);
            }
        }
        System.out.println();
        System.out.println("경우의 수 : " + answer);
    }
}
```



<h4>C++</h4>

```c++
#include <cstdio>
#define ll long long
using namespace std;

int main()
{
    ll answer = 0;
    ll a = 45;
    ll combination = 1;
    for (ll b = 45, c = 1; c <= 45; b--, c++)
    {
        combination = (combination * b) / c;
        if (c >= 15)
        {
            answer += combination;
            printf("45 C %lld = %lld\n", c, combination);
        }
    }
    printf("\n");

    printf("경우의 수 : %lld", answer);
    return 0;
}
```



<h4>출력 결과</h4>

```
45 C 15 = 344867425584
45 C 16 = 646626422970
45 C 17 = 1103068603890
45 C 18 = 1715884494940
45 C 19 = 2438362177020
45 C 20 = 3169870830126
45 C 21 = 3773655750150
45 C 22 = 4116715363800
45 C 23 = 4116715363800
45 C 24 = 3773655750150
45 C 25 = 3169870830126
45 C 26 = 2438362177020
45 C 27 = 1715884494940
45 C 28 = 1103068603890
45 C 29 = 646626422970
45 C 30 = 344867425584
45 C 31 = 166871334960
45 C 32 = 73006209045
45 C 33 = 28760021745
45 C 34 = 10150595910
45 C 35 = 3190187286
45 C 36 = 886163135
45 C 37 = 215553195
45 C 38 = 45379620
45 C 39 = 8145060
45 C 40 = 1221759
45 C 41 = 148995
45 C 42 = 14190
45 C 43 = 990
45 C 44 = 45
45 C 45 = 1

경우의 수 : 34901237112896
```

